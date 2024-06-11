# renovate-29521

Reproduction for <https://github.com/renovatebot/renovate/discussions/29521>.

## Current behavior

Renovate fails to process the OCIRepository:

```yaml
DEBUG: getManifestResponse(https://ghcr.io, kyverno/charts/kyverno, latest, head)
DEBUG: HEAD https://ghcr.io/v2/kyverno/charts/kyverno/manifests/latest = (code=ERR_NON_2XX_3XX_RESPONSE, statusCode=404 retryCount=0, duration=38)
DEBUG: Docker Manifest is unknown
{
  "err": {
    "name": "HTTPError",
    "code": "ERR_NON_2XX_3XX_RESPONSE",
    "timings": {
      "start": 1718120094776,
      "socket": 1718120094777,
      "lookup": 1718120094777,
      "connect": 1718120094786,
      "secureConnect": 1718120094795,
      "upload": 1718120094795,
      "response": 1718120094814,
      "end": 1718120094814,
      "phases": {
        "wait": 1,
        "dns": 0,
        "tcp": 9,
        "tls": 9,
        "request": 0,
        "firstByte": 19,
        "download": 0,
        "total": 38
      }
    },
    "message": "Response code 404 (Not Found)",
    "stack": "HTTPError: Response code 404 (Not Found)\n    at Request.<anonymous> (/usr/local/renovate/node_modules/.pnpm/got@11.8.6/node_modules/got/dist/source/as-promise/index.js:118:42)\n    at processTicksAndRejections (node:internal/process/task_queues:95:5)",
    "options": {
      "headers": {
        "user-agent": "RenovateBot/37.393.0 (https://github.com/renovatebot/renovate)",
        "authorization": "***********",
        "accept": "application/vnd.docker.distribution.manifest.list.v2+json, application/vnd.docker.distribution.manifest.v2+json, application/vnd.oci.image.manifest.v1+json, application/vnd.oci.image.index.v1+json",
        "accept-encoding": "gzip, deflate, br"
      },
      "url": "https://ghcr.io/v2/kyverno/charts/kyverno/manifests/latest",
      "hostType": "docker",
      "username": "",
      "password": "",
      "method": "HEAD",
      "http2": false
    },
    "response": {
      "statusCode": 404,
      "statusMessage": "Not Found",
      "body": "",
      "headers": {
        "content-type": "application/json",
        "docker-distribution-api-version": "registry/2.0",
        "date": "Tue, 11 Jun 2024 15:34:54 GMT",
        "content-length": "70",
        "x-github-request-id": "0A96:CE7B0:D567A2:F85713:66686E9E",
        "connection": "close"
      },
      "httpVersion": "1.1",
      "retryCount": 0
    }
  }
  "registryHost": "https://ghcr.io"
  "dockerRepository": "kyverno/charts/kyverno"
  "tag": "latest"
}

DEBUG: Could not determine new digest for update.
{
  "packageName": "ghcr.io/kyverno/charts/kyverno"
  "datasource": "docker"
}
```

## Expected behavior

Renovate parses the OCIRepository tag (3.2.3) and offer the 3.2.4 upgrade.
