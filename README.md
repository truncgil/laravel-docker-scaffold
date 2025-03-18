# Laravel Docker Scaffold

This project is a framework developed to quickly run Laravel applications on Docker. You can run your Laravel project in Docker containers with a single command.

## Advantages

- **Quick Setup**: Laravel environment running with a single command
- **Flexible Configuration**: Easily change settings like container names and ports
- **Portability**: Same development environment on different machines
- **Isolation**: Each project runs in its own containers

## Requirements

- Docker
- Docker Compose

## Kurulum (Installation)

### Repoyu Klonlama (Cloning the Repository)

1. GitHub reposunu bilgisayarınıza klonlayın:
   ```bash
   git clone https://github.com/truncgil/laravel-docker-scaffold.git
   ```

2. Klonladığınız dizine girin:
   ```bash
   cd laravel-docker-scaffold
   ```

3. (Opsiyonel) Yeni bir Laravel projesi başlatmak istiyorsanız, `.git` klasörünü silebilirsiniz:
   ```bash
   rm -rf .git
   ```

### Mevcut Bir Projede Kullanma

1. Mevcut Laravel projeniz için repoyu klonlayın:
   ```bash
   git clone https://github.com/truncgil/laravel-docker-scaffold.git temp-scaffold
   ```

2. Docker yapılandırma dosyalarını projenize kopyalayın:
   ```bash
   cp -r temp-scaffold/docker/ temp-scaffold/docker-compose.yml temp-scaffold/.env.example your-project/
   ```

3. Geçici klasörü silin:
   ```bash
   rm -rf temp-scaffold
   ```

## Initial Configuration

Before starting the containers, configure your environment variables:

1. Create a `.env` file by copying the `.env.example`:
   ```bash
   cp .env.example .env
   ```

2. Configure your application settings:
   ```ini
   # Application settings
   APP_NAME=YourAppName
   APP_PORT=7004            # The port your application will use
   APP_PREFIX=laravel       # Prefix for your container names
   
   # Database settings
   DB_DATABASE=your_database
   DB_USERNAME=your_username
   DB_PASSWORD=your_password
   ```

3. Customize other settings in the `.env` file according to your needs

## Installation and Usage

1. Clone this repository or copy the files to a new project (see detailed instructions above)
2. Run the following command:

```bash
docker-compose up -d
```

This command automatically starts:
- PHP/Laravel application container
- MySQL database container
- Nginx web server container

## Installing Dependencies

After the containers are running, to install Composer dependencies:

```bash
docker-compose exec app composer install
```

## Application Configuration

Complete the necessary steps for the Laravel application:

```bash
# Generate application key
docker-compose exec app php artisan key:generate

# Create database tables
docker-compose exec app php artisan migrate
```

## Customization

You can customize your application by editing the variables in the `.env` file:

- `APP_PORT`: The port on which the application will run (default: 7004)
- `APP_PREFIX`: Prefix for container and image names (default: laravel)

Example: If you set `APP_PREFIX=myproject`, the container names will be `myproject-app`, `myproject-db`, etc.

## Access

After completing the setup, you can access your application from your browser at:

```
http://localhost:7004
```

## Frequently Used Commands

### Viewing Container Logs

```bash
docker-compose logs
```

### Running Commands Inside the Container

```bash
docker-compose exec app php artisan <command>
```

### Stopping Containers

```bash
docker-compose down
```

### Restarting Containers

```bash
docker-compose restart
```

## Usage for New Projects

To use this framework in your new Laravel projects:

1. Copy this repository to your new project folder (see detailed cloning instructions above)
2. Change the `APP_PREFIX` value in the `.env` file to suit your project
3. Run the `docker-compose up -d` command
4. Install Composer dependencies and complete Laravel configurations