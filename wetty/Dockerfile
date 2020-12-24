FROM node:current-alpine as builder
RUN apk add -U build-base python git
WORKDIR /usr/src/app
RUN git clone https://github.com/butlerx/wetty /usr/src/app && \
    yarn && \
    yarn build && \
    yarn install --production --ignore-scripts --prefer-offline

FROM node:current-alpine
LABEL maintainer="None"
WORKDIR /usr/src/app
ENV NODE_ENV=production
EXPOSE 3000
COPY --from=builder /usr/src/app/build /usr/src/app/build
COPY --from=builder /usr/src/app/node_modules /usr/src/app/node_modules
COPY --from=builder /usr/src/app/package.json /usr/src/app/package.json
RUN apk add -U openssh-client sshpass && \
    mkdir ~/.ssh

ENTRYPOINT [ "yarn" , "docker-entrypoint"]
