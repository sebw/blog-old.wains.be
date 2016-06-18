# My SSH client configuration

```
Host *
        ForwardAgent yes
        # With Windows DC as DNS --> no
        GSSAPIAuthentication no
        AddressFamily inet
        IdentityFile ~/.ssh/id_rsa
        SendEnv LANG LC_*
        HashKnownHosts yes
        GSSAPIDelegateCredentials no
        EscapeChar ~
        ServerAliveInterval 60
        ServerAliveCountMax 60
        #User root

        # Check SSHFP record
        VerifyHostKeyDNS yes

        ControlMaster auto
        ControlPath ~/.ssh/ssh_socket_%h-%p-%r
        ControlPersist 5m
```
