#stage 1 builder
FROM node:20-alpine AS builder

WORKDIR /frontend

COPY package.json package-lock.json tsconfig.json .

RUN npm install

COPY public/ ./public/

COPY src/ ./src/

#stage 2 tests

FROM builder AS test
RUN npm run test -- --watchAll=false

# stage 3 final
FROM test AS final
EXPOSE 3000
ENTRYPOINT ["npm"]

CMD ["start"]

