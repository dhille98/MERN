# witing docker file for fonted applications 

FROM node:18.9.1

LABEL authoer="dhille"

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 5173

CMD [ "npm", "run", "dev" ]


