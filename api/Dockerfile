FROM datacat:latest
COPY wait-for-it/wait-for-it.sh /usr/bin/wait-for-it.sh
CMD ["/usr/bin/wait-for-it.sh", "api:7687", "--", "java", "--enable-preview", "org.springframework.boot.loader.JarLauncher"]
