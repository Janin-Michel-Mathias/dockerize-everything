FROM rustlang/rust:nightly-slim
EXPOSE 8000
WORKDIR /app

RUN apt update && \
	apt upgrade -y && \
	apt install -y libpq-dev && \
	cargo install diesel_cli --no-default-features --features postgres

COPY . .

RUN cargo install --path . && \
	cp /usr/local/cargo/bin/blog ./blog && \

CMD diesel migration run && ./blog
