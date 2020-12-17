FROM node:alpine as builder

# install and cache app dependencies
COPY ./package.json ./
RUN npm install && mkdir /phoenix-landing && mv ./node_modules ./phoenix-landing

WORKDIR /phoenix-landing

COPY . .

RUN npm run build



# ------------------------------------------------------
# Production Build
# ------------------------------------------------------
FROM nginx:1.16.0-alpine
COPY --from=builder /phoenix-landing/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
