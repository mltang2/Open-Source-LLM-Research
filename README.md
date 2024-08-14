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

ngrok config add-authtoken <TOKEN> \
ngrok http http://localhost:3000

Finally, a screen similar to one below will appear, and the link that can be used on any device to access your open source llms will be the link following "Forwarding".

<img width="396" alt="Screenshot 2024-07-27 at 11 16 06 AM" src="https://github.com/user-attachments/assets/f7ef78f3-21ce-4355-aef1-72d272792a68">


Once we discovered how to access any open source llm on any device, our next step was figure out if it was possible to run fine tuned versions of open source llms on Ollama as well. After digging a little deeper, we found that it was possible to download pre fine tuned open source llms from HuggingFace, and upload it onto Ollama. The process of doing so can be described below. \
\
To make things easier, I will be using an example model called jackalope which is a fine tuned version of the open source llm mistral that can be found on HuggingFace. Once on the model, find the GGUF quantized version of the model and download it. 

<img width="589" alt="Screenshot 2024-07-29 at 3 54 25 PM" src="https://github.com/user-attachments/assets/02e5de65-e75f-41f5-ae8e-3cd214c2c3b4"> <img width="861" alt="Screenshot 2024-07-29 at 3 55 01 PM" src="https://github.com/user-attachments/assets/3fe48963-ba15-41d8-9083-12caf59360ac">

Once downloaded, open back the terminal and run the command "ollama show '*model name*' –modelfile". Since my model name in this case was mistral, a template similar to the one will show up. 
\
<img width="326" alt="Screenshot 2024-08-09 at 12 59 08 PM" src="https://github.com/user-attachments/assets/5010708d-0325-47e8-ae7b-266db2affa69">

Open a nano document, and paste the template into it. Save the template, then exit out of it. Finally, in the terminal run the line "ollama create '*whatever name you choose*' -f ./'*name of nano document*'"
From there simiply do "ollama run '*whatever name you chose*'" and you will have sucessfully created and ran your fine tuned llm. 
\
\
The next question we were looking to answer was what how could we best quantize a fine tuned open source llm while being mindful of time, space, hardware, and memory. The end goal was to allow students to easily quantize models to GGUF, and we understood that many students had differents types of devices, older or newer. After a bit of searching, we decided that it would be best to use a resource that was cloud-based. We came across a Google Colab Notebook and decided to try it out. This fit our criteria as it was a free, cloud-based platform, and offered everyone access to a GPU and TPU. 
https://colab.research.google.com/drive/13dVitv_DBCTprbCarKwFJdf8qG76y6hD?usp=sharing#scrollTo=fCUkxVOhHyso 
\
Above is the link to the Google Colab. Essentially, this notebook gives a template to automate setting up and quantizing a model. The template does this by handling model loading, environment setup, model quantization, and finally uploading the model to hugginface.

