# syntax=docker/dockerfile:1

## Example: run tini first, as PID 1

FROM node:23-bookworm-slim

# replace npm in CMD with tini for better kernel signal handling
ENV NODE_ENV=production
ENV TINI_VERSION=v0.19.0
ADD --chmod=755 https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/local/bin/tini

# set entrypoint to always run commands with tini
ENTRYPOINT ["/usr/local/bin/tini", "--"]

EXPOSE 3000

USER node

WORKDIR /app

COPY --chown=node:node package*.json ./

RUN npm ci --omit=dev && npm cache clean --force

COPY --chown=node:node . .

CMD ["node", "index.js"]
