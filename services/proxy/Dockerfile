ARG VERSION=latest

FROM bentrm/datacat-editor:${VERSION} AS build
RUN npm run-script build

FROM nginx:stable-alpine
COPY --from=build /app/build/ /var/www
COPY nginx.conf /etc/nginx/templates/default.conf.template
