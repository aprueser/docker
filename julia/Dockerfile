FROM julia:1.8.2-bullseye

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
                vim \
                git \
		ssh \
	; \
	rm -rf /var/lib/apt/lists/*

# Copy a .vimrc file into the container with basic settings
COPY ./julia_vimrc /root/.vimrc

RUN set -eux; \
# Install Julia Vim plugin
        curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim; \
        vim -es -u /root/.vimrc -i NONE -c "PlugInstall" -c "qa"; \
# Install some Julia packages
	julia -e 'using Pkg; Pkg.update()'; \
        julia -e 'using Pkg; Pkg.add.(["AbstractTrees", "Actors", "ArgCheck", "ArgParse", "Avro", "BenchmarkTools", "Chain", "CSV", "DataFrames", "DataFramesMeta", "DataStructures", "Dates", "DuckDB", "ErrorTypes", "HTTP", "InMemoryDatasets", "JSON3", "LazyArrays", "LazyJSON", "Logging", "MethodAnalysis", "MiniLoggers", "Parameters", "Parquet", "PkgTemplates", "Random", "Redis", "ResultTypes", "Revise", "RDKafka", "StatsBase", "StructTypes", "Temporal", "TimeSeries", "TimeZones", "XLSX"])'; \
	julia -e 'using Pkg; Pkg.precompile()'; \
# smoke test
	julia --version

CMD ["julia"]
