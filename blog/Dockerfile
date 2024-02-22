FROM rustlang/rust:nightly-slim

WORKDIR /app

RUN apt update && apt upgrade -y

RUN apt install -y libpq-dev

RUN rustup override set nightly

COPY . .

RUN cargo install --path .

RUN cp /usr/local/cargo/bin/blog ./blog

RUN cargo install diesel_cli --no-default-features --features postgres

EXPOSE 8000

CMD diesel migration run && ./blog




