# from which image
FROM nginx

# what to copy into the container from localhost
COPY index.html /usr/share/nginx/html

# port 80
EXPOSE 80

# CMD specific instructions
CMD ["nginx", "-g", "daemon off;"]
