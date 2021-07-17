## API Conversão Kube Dev

```
docker build -t mhfa/api-conversao:v0.0.1 .
docker tag mhfa/api-conversao:v0.0.1 mhfa/api-conversao:latest
docker run -p 8080:8080 mhfa/api-conversao
```