FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
RUN addgroup --group simulator --gid 2000 && adduser --uid 1000 --gid 2000 --disabled-password --gecos '' "simulator"
RUN mkdir /workspace
RUN chown -R simulator:simulator /app
RUN chown -R simulator:simulator /workspace
RUN apt update; \
    apt install -y sqlite3
USER simulator:simulator
COPY * /app/
EXPOSE 17070-17077
ENTRYPOINT ["/app/Tricentis.Simulator.Agent", "/workspace", "-p 17070"]
