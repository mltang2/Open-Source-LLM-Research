# Open-Source-LLM-Research
With professor Dr. George Thomas, we spent the summer diving deep into how we can access open source large language models, fine tune them, and integrate them into existing applications. Here is what we found!

While it was possible to have applications access the interface programatically, it was easiest to incorporate applications that already had functionalities that could download and run different llms efficiently. After playing around with multiple platforms including UnionCloud, TensorFlow, and Ollama, we ultimately decided to continue with Ollama. The main reason for this choice was because of the ease of use that Ollama provided. With its potential for local execution with hundreds of open source models, mixed in with its endless possibilities for customization, versatility, and integration, we discovered that Ollama was the best platform to run large language models. 
https://github.com/ollama/ollama 

After a few days of running different llms like llama3, gemma, and mistral, we decided to look further into how we could access them on other devices without needing to redownload the llms and the ollama platofrm. We found out that by installing and using docker as well as ngrok, we would be able to run our local host on any device. First, you would want to paste http://127.0.0.1:11434/ into your browser in order to make sure that ollama is running succesfully on your local host. Next, you want to download docker at https://docs.docker.com/desktop/install/mac-install/ 

After installation, you want to run the following commands:
docker run -d \
-p 3000:8080 \
--add-host=host.docker.internal:host-gateway \
-v open-webui:/app/backend/data \
--name open-webui \
--restart always \
ghcr.io/open-webui/open-webui:main 

You can check if everything is still working correctly by pasting http://127.0.0.1:3000/auth into a web browser. Once ngrok is downloaded https://ngrok.com/download , find your token on ngrok, and type the following commands in your terminal:

ngrok config add-authtoken <TOKEN> 
ngrok http http://localhost:3000

Finally, a screen similar to one below will appear, and the link that can be used on any device to access your open source llms will be the link following "Forwarding".

<img width="396" alt="Screenshot 2024-07-27 at 11 16 06 AM" src="https://github.com/user-attachments/assets/f7ef78f3-21ce-4355-aef1-72d272792a68">


