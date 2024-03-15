# Prueba Nuestro Asistente!

Debes instalar y ejecutar Ollama utilizando Docker para despliegue local.

## Instalación de Ollama

1. Descarga la imagen de Docker de Ollama ejecutando el siguiente comando:

```bash
docker pull ollama/ollama
```

2. Ejecuta el contenedor:

```bash
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

3. Descarga el modelo de lenguaje 'llama2':

```bash
docker exec -it ollama ollama pull llama2
```

## Clona el repositorio:

```bash
gh repo clone DotNet-Ecuador/ollama-labwork
cd ollama-labwork
```

### Crea 'dotnet-community-assistant' basado en 'llama2'

```bash
docker cp ./Modelfile ollama:.
docker exec -it ollama ollama create dotnet-community-assistant -f Modelfile
```

## Ejecuta el modelo en la terminal

```bash
docker exec -it ollama ollama run dotnet-community-assistant
```

## REST API

```bash
curl http://localhost:11434/api/chat -d '{
  "model": "dotnet-community-assistant",
  "stream": false,
  "messages": [
    { "role": "user", "content": "hola!" }
  ]
}'
```

```bash
{
  "model": "dotnet-community-assistant",
  "created_at": "2024-03-14T22:40:02.228724525Z",
  "message": {
    "role": "assistant",
    "content": "Hola! Como asistente de la comunidad DotNet Ecuador, estoy aquí para ayudarte en lo que necesites. ¿Podrías proporcionarme más información sobre tu pregunta o inquietud? Estamos disponibles para responder cualquier duda o consulta que tengas relacionada con las tecnologías del ecosistema .NET y la comunidad DotNet Ecuador."
  },
  "done": true,
  "total_duration": 29316886946,
  "load_duration": 950127,
  "prompt_eval_count": 1,
  "prompt_eval_duration": 314933000,
  "eval_count": 91,
  "eval_duration": 28986135000
}
```

## Instalación de Open WebUI (Opcional)

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

Accede a http://localhost:3000/ en tu navegador web.
Completa el proceso de registro en Open WebUI.
Selecciona el modelo de lenguaje 'dotnet-community-assistant'.

¡Listo! Ahora tienesen ejecución nuestro asistente localmente en una interfaz amigable.

<img width="960" alt="image" src="https://github.com/DotNet-Ecuador/ollama-labwork/assets/57963142/3c3848a2-e090-47bc-902f-60099860cdc0">

