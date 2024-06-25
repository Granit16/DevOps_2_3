

source "yandex" "debian_docker" {
  disk_type           = "network-hdd"
  folder_id           = "b1cne6pe0gtegmbo514u"
  image_description   = "my custom debian with docker"
  image_name          = "debian-11-docker"
  source_image_family = "debian-11"
  ssh_username        = "debian"
  subnet_id           = "e9bdfla76jdakjd7fpn8"
  token               = "y0_AgDl5kB_UXlO9AATuwQAAhA662AAAAALtAAEIZ4HdAA_poDDbWULpwvqSQ"
  use_ipv4_nat        = true
  zone                = "ru-central1-a"
}

build {
  sources = ["source.yandex.debian_docker"]

  provisioner "shell" {
    inline = [
      "echo 'hello from packer'",
"export DEBIAN_FRONTEND=noninteractive",
"# Add Docker's official GPG key:",
"sudo apt-get update",
"sudo apt-get install -y ca-certificates curl gnupg",
"sudo install -m 0755 -d /etc/apt/keyrings",
"curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg",
"sudo chmod a+r /etc/apt/keyrings/docker.gpg",
"# Add the repository to Apt sources:",
"echo \"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian bullseye stable \" |  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null",
"sudo apt-get update",
"sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin",
"sudo apt-get install -y htop tmux"
    ]
  }

}

