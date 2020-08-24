ARG VERSION=latest

FROM bentrm/datacat-explorer:${VERSION} AS build
ARG VERSION
ARG TITLE
ARG MAIL
ENV REACT_APP_VERSION=${VERSION}
ENV REACT_APP_TITLE=${TITLE}
ENV REACT_APP_MAIL=${MAIL}
RUN npm run-script build

FROM nginx:stable-alpine
COPY --from=build /app/build/ /var/www
COPY nginx.conf /etc/nginx/templates/default.conf.template
