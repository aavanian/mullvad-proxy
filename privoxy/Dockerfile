FROM alpine:3.24

# Alpine ships the stock privoxy config as *.new files; only the listen
# address needs changing so other containers can reach it. Logging goes to
# stderr so it shows up in `docker logs`.
RUN apk upgrade --no-cache && \
    apk add --no-cache privoxy && \
    for f in /etc/privoxy/*.new; do mv "$f" "${f%.new}"; done && \
    sed -i -e 's/^listen-address .*/listen-address  0.0.0.0:8118/' \
           -e '/^logfile /d' /etc/privoxy/config

EXPOSE 8118

ENTRYPOINT ["privoxy", "--no-daemon", "--user", "privoxy", "/etc/privoxy/config"]
