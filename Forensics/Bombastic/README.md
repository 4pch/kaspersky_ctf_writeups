# Writeup

Author's solution to Bombastic challenge

    As obvious from the description, check dockerhub for a container named bombastic

The container itself has a python module which is protected by pyarmor. Going straight with it might be harder and more time consuming, so it's better to check other datasources firstCheck OCI using oras discover docker.io/kaspctf/bombastic:latestFrom there you can find application/vnd.sbom+json with the digest sha256:cc42156be710c5d25a13772fea31e48ef41b34ea88893e31cc22df77939fed12oras pull docker.io/kaspctf/bombastic@sha256:cc42156be710c5d25a13772fea31e48ef41b34ea88893e31cc22df77939fed12 -o out-dirRead sbom.jsom where you can find
```
{
      "bom-ref": "requirements-L117",
      "description": "requirements line 117: super-duper-secret-malicious-dependencie==0.2.0     --hash=sha256:38e3c2a987d69be26449b2f287b4d370f8db331cafbb7f57d04cb157d58b51eb     --hash=sha256:e44ac2cd1ac5e53f063052056fef2b48defcc14d35d8e8009b411f6e66c9c186",
      "externalReferences": [
        {
          "comment": "implicit dist url",
          "hashes": [
            {
              "alg": "SHA-256",
              "content": "38e3c2a987d69be26449b2f287b4d370f8db331cafbb7f57d04cb157d58b51eb"
            },
            {
              "alg": "SHA-256",
              "content": "e44ac2cd1ac5e53f063052056fef2b48defcc14d35d8e8009b411f6e66c9c186"
            }
          ],
          "type": "distribution",
          "url": "https://pypi.org/simple/super-duper-secret-malicious-dependencie/"
        }
      ],
      "name": "super-duper-secret-malicious-dependencie",
      "purl": "pkg:pypi/super-duper-secret-malicious-dependencie@0.2.0",
      "type": "library",
      "version": "0.2.0"
    },
```

    The malicious package is already removed from the pypi, but using the hash you can check if it's been uploaded to virustotal (which happens automatically for all packages)

 

    It is indeed uploaded to VT, which has scanned the code and has the backdoor details in the code insights
    <img width="1275" height="219" alt="image" src="https://github.com/user-attachments/assets/4270713e-edfe-4097-967f-6d89b99193d6" />

