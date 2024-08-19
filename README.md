# canvas-deploy

1. Grant access to the data store for the container
```bash
mkdir .data && sudo chmod -R 777 .data
```

1. Start only the database container
```bash
docker compose up -d db
```

1. Initialize the database
```bash
docker compose run --rm app bundle exec rake db:create db:initial_setup
```

1. Start all containers
```bash
docker compose up -d
```

1. Open a shell inside the canvas-lms_app_1 container to finish setup
```bash
docker exec -u root -it canvas-lms_app_1 /bin/bash
```

1. Build all Canvas assets
```bash
bundle exec rake canvas:compile_assets
bundle exec rake brand_configs:generate_and_upload_all
exit
```

1. Visit (http://localhost:8900)[http://localhost:8900]
