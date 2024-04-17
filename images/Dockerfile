FROM mcr.microsoft.com/dotnet/runtime-deps:6.0-jammy as build

RUN apt-get update -y
RUN apt-get install -y sysvbanner

FROM ghcr.io/actions/actions-runner:latest

COPY --from=build /usr/bin/banner /usr/bin/banner

