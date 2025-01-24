# Webapp text demo container: Reuses the api-server image 
# (see ../api-server/Dockerfile and ensure it is built first).

# To run the container:
# docker run --gpus all -it --rm -p 8000:8000 minicpm-o_2.6-api-server:latest python /root/MiniCPM-o/web_demos/minicpm-o_2.6/chatbot_web_demo_o2.6.py