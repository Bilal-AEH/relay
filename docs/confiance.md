# PKI — Infrastructure à clé publique

## Le problème

Comment prouver son identité sur un réseau à quelqu'un qui ne vous connaît pas ?

## Architecture

La PKI (Public Key Infrastructure) repose sur une hiérarchie de confiance :

```
CA Racine (Root CA)
    └── CA Intermédiaire
            └── Certificat serveur
```

La **CA Racine** est auto-signée et pré-installée dans les systèmes d'exploitation. Elle ne signe directement que les CA intermédiaires — jamais les certificats finaux.

La **CA Intermédiaire** signe les certificats des serveurs. Si elle est compromise, on peut la révoquer sans toucher à la CA racine.

Le **certificat serveur** contient : la clé publique du serveur, son nom de domaine, sa date d'expiration, et la signature de la CA intermédiaire.

## Vérification d'un certificat TLS

```python
import ssl, socket

context = ssl.create_default_context()
with socket.create_connection(("github.com", 443)) as sock:
    with context.wrap_socket(sock, server_hostname="github.com") as ssock:
        cert = ssock.getpeercert()
        print(cert['subject'])
        print(cert['notAfter'])
```

Python vérifie automatiquement : la signature de la chaîne, la date d'expiration, le nom de domaine. Si l'un échoue — `ssl.SSLCertVerificationError`.

## Révocation

Un certificat compromis doit être révoqué avant son expiration. Deux mécanismes :

- **CRL (Certificate Revocation List)** — liste publiée périodiquement par la CA
- **OCSP (Online Certificate Status Protocol)** — vérification en temps réel

## Voir dans le projet

- Session 01 : la confiance transitive et son parallèle humain
