# syntax=docker/dockerfile:1

## Example: The most basic, CORRECT, Dockerfile for Node.js

# always use slim images
FROM node:23-bookworm-slim

EXPOSE 3000

# add user first, then set WORKDIR to set permissions
USER node

# WORKDIR now actually assigns proper permissions based on the user above it
WORKDIR /app

# copy in with correct permissions. Using * prevents errors if file is missing
COPY --chown=node:node package*.json ./

# use ci to only install packages from lock files
RUN npm ci --omit=dev && npm cache clean --force

# copy files with correct permissions
COPY --chown=node:node . .

# change command to run node directly
CMD ["node", "index.js"]
