[ HOME ](README.md)
# Read 34 - API Deployment

# Configuring Django Settings: Best Practices

### Managing Django Settings: Issues
- Different environments.
- Sensitive data.
- Sharing settings between team members.
- Django settings are a Python code.

### Setting Configuration: Different Approaches
- settings_local.py
    - Pros:
      -  1 Secrets not in VCS.
    - Cons:
      - settings_local.py is not in VCS, so you can lose some of your Django environment settings.
      - The Django settings file is a Python code, so settings_local.py can have some non-obvious logic.
      - You need to have settings_local.example (in VCS) to share the default configurations for developers.
- Separate settings file for each environment
  ```
  settings/
    ├── __init__.py
    ├── base.py
    ├── ci.py
    ├── local.py
    ├── staging.py
    ├── production.py
    └── qa.py
  ```

  - Pros:
    - All environments are in VCS.
    - It’s easy to share settings between developers.
  - Cons:
    - You need to find a way to handle secret passwords and tokens.
    - “Inheritance” of settings can be hard to trace and maintain.
- Environment variables.
  - To solve the issue with sensitive data, you can use environment variables.
  - Issues:
    - You need to handle KeyError exceptions.
    - You need to convert types manually.
  - Pros:
    - Configuration is separated from code.
    - Environment parity – you have the same code for all environments.
    - No inheritance in settings, and cleaner and more consistent code.
    - There is a theoretical grounding for using environment variables – 12 Factors.
  - Cons:
    - You need to handle sharing default config between developers.


### 12 Factors

> 12 Factors is a collection of recommendations on how to build distributed web-apps that will be easy to deploy and scale in the Cloud.

Its main rule is to **store configuration in the environment.**

1. Codebase
1. Dependencies
1. Config
1. Backing services
1. Build, release, run
1. Processes
1. Port binding
1. Concurrency
1. Disposability
1. Dev/prod parity
1. Logs
1. Admin processes

### django-environ
Environment variables are the perfect place to store settings.
This app gives a well-functioning API for reading values from environment variables or text files, handful type conversion, etc.

Instead of splitting settings by environments, you can split them by the source: Django, third- party apps (Celery, DRF, etc.), and your custom settings.

File structure:
```
project/
├── apps/
├── settings/
│   ├── __init__.py
│   ├── djano.py
│   ├── project.py
│   └── third_party.py
└── manage.py
```

# SSH (AKA Secure Shell)

> Is a remote administration protocol that allows users to control and modify their remote servers over the Internet. 

- The service was created as a secure replacement for the unencrypted Telnet and uses cryptographic techniques to ensure that all communication to and from the remote server happens in an encrypted manner. 
- It provides a mechanism for authenticating a remote user, transferring inputs from the client to the host, and relaying the output back to the client.

The significant advantage offered by SSH over its predecessors is the use of encryption to ensure secure transfer of information between the host and the client. Host refers to the remote server you are trying to access, while the client is the computer you are using to access the host. There are three different encryption technologies used by SSH:

1. Symmetrical encryption
1. Asymmetrical encryption
1. Hashing.


### Symmetric Encryption (AKA shared key or shared secret encryption.)

- Form of encryption where a secret key is used for both encryption and decryption of a message by both the client and the host. 
- Effectively, any one possessing the key can decrypt the message being transferred.
- The secret token is specific to each SSH session, and is generated prior to client authentication. 

![](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/symmetric-encryption-ssh-tutorial.jpg)

### Asymmetric Encryption
- Asymmetrical encryption uses two separate keys for encryption and decryption. These two keys are known as the public key and the private key. 
- Together, both these keys form a public-private key pair.

![](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/asymmetric-encryption.jpg)

- The public key, as the name suggest is openly distributed and shared with all parties. 
- While it is closely linked with the private key in terms of functionality, the private key cannot be mathematically computed from the public key. 
- The relation between the two keys is highly complex: a message that is encrypted by a machine’s public key, can only be decrypted by the same machine’s private key. 
- This one-way relation means that the public key cannot decrypt its own messages, nor can it decrypt anything encrypted by the private key.

### Hashing
- One-way-hash functions generate a unique value of a fixed length for each input that shows no clear trend which can exploited. This makes them practically impossible to reverse.

![](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/ssh-tutorial-hash.jpg)

-SSH uses hashes to verify the authenticity of messages. 
- This is done using HMACs, or Hash-based Message Authentication Codes. This ensures that the command received is not tampered with in any way.

## How Does SSH Work with These Encryption Techniques
The way SSH works is by making use of a client-server model to allow for authentication of two remote systems and encryption of the data that passes between them.

![](https://www.hostinger.com/tutorials/wp-content/uploads/sites/2/2017/07/ssh-client-and-server.jpg)