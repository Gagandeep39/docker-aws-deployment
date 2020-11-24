FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

# Provided for documentatin purpose
# makes it easy to ovverride while running 
ENV MONGODB_USERNAME=gagan
ENV MONGODB_PASSWORD=123456
ENV MONGODB_URL=mongodb

CMD ["npm", "start"]
