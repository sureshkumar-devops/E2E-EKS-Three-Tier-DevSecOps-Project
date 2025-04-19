FROM node:18-bullseye-slim AS frontend
WORKDIR /app
COPY /app/frontend/package*.json ./
RUN npm install
COPY /app/frontend/ ./
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build


FROM node:18-alpine3.18
WORKDIR /app
COPY --from=frontend /app/package.json /app/
COPY --from=frontend /app/node_modules /app/node_modules
COPY --from=frontend /app/public /app/public
COPY --from=frontend /app/src /app/src
CMD ["npm", "start"]