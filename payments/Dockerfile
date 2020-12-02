FROM node:14.4.0-alpine3.11
ENV NODE_ENV=production
ENV VAR1=securitynewssourcepayments-dev

RUN mkdir -p /opt/sns/app && \
    mkdir -p /opt/sns/logs && \
    chmod 700 /opt/sns/logs

COPY config /opt/sns/app/config 
COPY controllers /opt/sns/app/controllers
COPY domain /opt/sns/app/domain
COPY repositories /opt/sns/app/repositories
COPY package*.json /opt/sns/app/
COPY server.js /opt/sns/app/
COPY docker-entrypoint.sh /opt/sns/app/

COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent && mv node_modules ../

WORKDIR /opt/sns/app

RUN chmod 700 docker-entrypoint.sh && \
    npm install

EXPOSE 3000

ENTRYPOINT ["./docker-entrypoint.sh"]

CMD ["node", "server.js"]


