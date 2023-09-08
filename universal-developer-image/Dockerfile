FROM quay.io/devfile/universal-developer-image:ubi8-latest

USER 0
RUN dnf update -y && dnf install -y postgresql-odbc unixODBC unixODBC-devel

USER 10001
