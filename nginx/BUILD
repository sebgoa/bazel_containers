load("@io_bazel_rules_docker//docker:docker.bzl", "docker_build", "docker_push")

docker_build(
    name = "nginx",
    labels = {"maintainer" : "Bitnami <containers@bitnami.com>"},
    base = "@bitnami_minideb//image:image.tar",
    debs = [
        "@glibc//file",
    ],
    symlinks = {
        "/opt/bitnami/nginx/html" : "/app",
    },
    env = {
        "BITNAMI_APP_NAME" : "nginx",
        "BITNAMI_IMAGE_VERSION" : "1.12.0-r3",
        "NGINX_HTTPS_PORT_NUMBER" : "443",
        "NGINX_HTTP_PORT_NUMBER" : "80",
        "PATH" : "/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/opt/bitnami/nami/bin:/opt/bitnami/nginx/sbin:$PATH",
    },
    ports = ["80", "443"],
    volumes = ["/bitnami/nginx"],
    workdir = "/app",
    entrypoint = ["/entrypoint.sh"],
    cmd = ["/run.sh"],
    files = ["entrypoint.sh", 
             "run.sh", 
             "nginx-inputs.json",
             "@nginx_bitnami//file"],
)

docker_push(
   name = "push_nginx",
   image = ":nginx",
   registry = "gcr.io",
   repository = "skippbox/bazel",
   tag = "dev",
)
