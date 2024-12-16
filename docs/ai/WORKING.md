# This is work

Run this command to pull the contaier and start it
```bash
sudo docker run -d -p 3000:8080 -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

Run this command to enter the contaier to pull ollama Models
```bash
sudo docker exec -it * bash
```
Replace the * with the docker contaier name