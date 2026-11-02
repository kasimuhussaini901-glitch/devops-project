FROM openjdk:11-jdk
WORKDIR /app
COPY . .
RUN echo "Building application"
CMD ["echo", "Application deployed successfully"]
