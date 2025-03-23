# Docker:

## How to:
#### Add secrets:
Sukurt `docker-compose.yaml` (pvz. apacioj). `my-secret-app` build time'e sukurs kintamuosius `marta` ir `secret_2`:  
- `marta` verte yra `/run/secrets/my_secret` content'e. File'as yra sukuriamas is zemiau esancio secrets.txt. T.y.: `secrets.txt` > `my_secret` yra reference > `/run/secrets` yra sukuriam'a automatiskai Docker compose
- `secret_2` gana aisku, definiuojam ji kaip bash'ui

```yaml
services:
  my-secret-app:
    image: docker/secrets
    environment:
      marta: /run/secrets/my_secret
      secret_2: slaptazodis_secret_2
    secrets:
      - my_secret

secrets:
  my_secret:
    file: secrets.txt
  secret_2:
    file: secret_2.txt
```

# URLs:
Use secrets: 
- https://docs.docker.com/compose/how-tos/use-secrets/

Use environment variables in Compose:
- https://docs.docker.com/compose/how-tos/environment-variables/#/the-env-file
