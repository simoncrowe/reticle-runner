# shortlist-runner

HTTP service that validates profile payloads against [shortlist-schema](https://github.com/simoncrowe/shortlist-schema) and creates Kubernetes batch jobs to assess them. Runs in-cluster on port 8080.

## API

- `POST /api/v1/profiles` - Submit a profile for assessment. Returns `201` with `{"id": "assessor-<uuid>"}`.
- `GET /health` - Liveness probe.

## Configuration

All via environment variables:

| Variable | Description |
|---|---|
| `ASSESSOR_CONFIG_PATH` | Path to assessor config file |
| `ASSESSOR_IMAGE` | Assessor container image |
| `ASSESSOR_CACHE_BUCKET_NAME` | GCS bucket for cache volume |
| `ASSESSOR_SERVICE_ACCOUNT` | K8s service account for assessor pods |
| `ASSESSOR_NODE_SELECTOR_KEY` | Node selector key for scheduling |
| `ASSESSOR_NODE_SELECTOR_VALUE` | Node selector value for scheduling |
| `NOTIFIER_URL` | Job completion notification URL |

## Development

### Running tests

```sh
go test ./...
```

### Building the Docker image

```sh
docker build -f docker/Dockerfile -t shortlist-runner .
```

## License

[MIT](LICENSE)
