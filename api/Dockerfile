ARG VERSION

FROM bentrm/datacat:${VERSION}
COPY wait-for-it/wait-for-it.sh /usr/bin/wait-for-it.sh
CMD ["/usr/bin/wait-for-it.sh", "db:7687", "-t", "60", "--", "java", "--enable-preview", "org.springframework.boot.loader.JarLauncher"]
