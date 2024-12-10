#
# Licensed under the Apache License, Version 2.0 (the “License”);
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#         http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an “AS IS” BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


# Node build
FROM node:20 AS build
RUN mkdir /app
WORKDIR /app
COPY ./*.json /app/
RUN npm install --silent
COPY ./src /app/src
COPY ./public /app/public
COPY ./src/config.ts.template /app/src/config.ts
RUN NODE_OPTIONS=--max-old-space-size=1536 npm run build
RUN ls /app/build

# Main Image
FROM openresty/openresty:1.25.3.2-1-alpine
RUN apk add gettext curl
# React
RUN rm /etc/nginx/conf.d/default.conf
COPY --from=build /app/build /usr/share/nginx/html
COPY ./nginx-wrapper.sh /etc/nginx/nginx-wrapper.sh
COPY ./nginx.conf.template /etc/nginx/conf.d/default.conf.template
COPY ./nginx.ssl.conf.template /etc/nginx/conf.d/default.ssl.conf.template
RUN mkdir -p /app
COPY ./certs /app/certs
RUN echo "daemon off;" >> /usr/local/openresty/nginx/conf/nginx.conf
EXPOSE 80
EXPOSE 443

CMD [ "/etc/nginx/nginx-wrapper.sh" ]
