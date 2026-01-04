# 🐻 Bear Presets

Community-maintained presets for [Bear](https://github.com/IRevolve/Bear) - the monorepo CI/CD tool.

## Usage

Bear automatically fetches presets from this repository:

```yaml
# bear.config.yml
name: my-project

use:
  languages: [go, node, python]
  targets: [docker, cloudrun, lambda]
```

## Available Presets

### Languages

| Preset | Detection | Description |
|--------|-----------|-------------|
| `go` | `go.mod` | Go with mod download, vet, test, build |
| `node` | `package.json` | Node.js with npm |
| `typescript` | `tsconfig.json` | TypeScript with tsc |
| `python` | `requirements.txt`, `pyproject.toml` | Python with pip, ruff, pytest |
| `rust` | `Cargo.toml` | Rust with cargo |
| `java` | `pom.xml`, `build.gradle` | Java with Maven/Gradle |

### Targets

| Preset | Description |
|--------|-------------|
| `docker` | Docker build & push |
| `cloudrun` | Google Cloud Run (service) |
| `cloudrun-job` | Google Cloud Run (job) |
| `lambda` | AWS Lambda |
| `s3` | AWS S3 sync |
| `s3-static` | S3 + CloudFront static site |
| `kubernetes` | Kubernetes kubectl |
| `helm` | Helm charts |
| `fly` | Fly.io |
| `vercel` | Vercel |
| `netlify` | Netlify |

## Contributing

1. Fork this repository
2. Add your preset in `languages/` or `targets/`
3. Update `index.yml`
4. Submit a PR

### Language Preset Format

```yaml
# languages/mylang.yml
name: mylang
detection:
  files: [mylang.config]
  # or pattern: "*.ml"
validation:
  setup:
    - name: Install deps
      run: mylang install
  lint:
    - name: Lint
      run: mylang lint
  test:
    - name: Test
      run: mylang test
  build:
    - name: Build
      run: mylang build
```

### Target Preset Format

```yaml
# targets/mytarget.yml
name: mytarget
defaults:
  REGION: us-east-1
  MEMORY: 256Mi
deploy:
  - name: Build
    run: mytarget build $NAME:$VERSION
  - name: Deploy
    run: mytarget deploy $NAME --region $REGION
```

## License

MIT
