# docker_ascp4
Aspera Connect ascp4 in Ubuntu 22.04

Aspera Connect version 4.2 (ascp) requires an operating environment of CentOS 8 or later.

Release Notes: IBM Aspera Connect 4.2.4
- [https://www.ibm.com/docs/en/aspera-connect/4.2?topic=release-notes-aspera-connect-424](https://www.ibm.com/docs/en/aspera-connect/4.2?topic=release-notes-aspera-connect-424)

Since the National Institute of Genetics supercomputer runs on CentOS 7, ascp cannot be operated as it is.

Therefore, I tried creating an Apptainer (formerly Singularity) container image for `ascp`. By placing this on the National Institute of Genetics supercomputer, you can use `ascp`. Place the container image in an appropriate location within your home directory on the supercomputer as follows:

```
cd $HOME
wget https://raw.githubusercontent.com/nig-sc/docker_ascp4/main/ascp4_ubuntu22.sif
```

Aspera Connect's installer needs to be run with user privileges and is installed under $HOME/.aspera, so installation is necessary the first time. The following command will install the ascp command:

```
$ apptainer exec ascp4_ubuntu22.sif bash /usr/local/src/ibm-aspera-connect_4.2.4.265_linux.sh

Installing IBM Aspera Connect

Deploying IBM Aspera Connect (/home/you/.aspera/connect) for the current user only.
Unable to register protocol handler, IBM Aspera Connect won't be able to auto-launch
Unable to register protocol handler, IBM Aspera Connect won't be able to support Faspex 5 transfers
Unable to update desktop database, IBM Aspera Connect may not be able to auto-launch

Install complete.
```

You can execute the ascp command as follows:

```
$ apptainer exec ascp4_ubuntu22.sif $HOME/.aspera/connect/bin/ascp --help
Usage: ascp [OPTION] SRC... DEST
          SRC to DEST, or multiple SRC to DEST dir
          SRC, DEST format: [[user@]host:]PATH
  -h,--help                       Display usage
  -A,--version                    Display version.
  -T                              Disable encryption
  -d                              Create target directory, implied for file/file-pair lists
  -p                              Preserve file timestamp
  -q                              Disable progress display
  -v                              Verbose mode
(continued below)
```

---
# docker_ascp4
Aspera Connect ascp4 in Ubuntu 22.04

Aspera Connect ver 4.2 (ascp)はCent OS 8以降の実行環境が必要です。

Release Notes: IBM Aspera Connect 4.2.4
- https://www.ibm.com/docs/en/aspera-connect/4.2?topic=release-notes-aspera-connect-424

遺伝研スパコンはCent OS 7で動いているので、このままではascpを動作させることができません。

そこで`ascp`のApptainer (旧Singularity)コンテナイメージを作ってみました。これを遺伝研スパコン上に設置することで`ascp`を使うことができます。
以下のようにしてコンテナイメージを遺伝研スパコンのホームディレクトリ中の適当な場所に置きます。

```
cd $HOME
wget  https://raw.githubusercontent.com/nig-sc/docker_ascp4/main/ascp4_ubuntu22.sif
```

Aspera Connectのインストーラはユーザ権限で実行する必要があり、$HOME/.asperaの下にインストールされるので、
最初の一回はインストール作業が必要です。以下のコマンドによりascpコマンドがインストールされます。

```
$ apptainer exec ascp4_ubuntu22.sif bash /usr/local/src/ibm-aspera-connect_4.2.4.265_linux.sh

Installing IBM Aspera Connect

Deploying IBM Aspera Connect (/home/you/.aspera/connect) for the current user only.
Unable to register protocol handler, IBM Aspera Connect won't be able to auto-launch
Unable to register protocol handler, IBM Aspera Connect won't be able to support Faspex 5 transfers
Unable to update desktop database, IBM Aspera Connect may not be able to auto-launch

Install complete.
```

以下のようにするとascpコマンドを実行することができます。

```
$ apptainer exec ascp4_ubuntu22.sif  $HOME/.aspera/connect/bin/ascp --help
Usage: ascp [OPTION] SRC... DEST
          SRC to DEST, or multiple SRC to DEST dir
          SRC, DEST format: [[user@]host:]PATH
  -h,--help                       Display usage
  -A,--version                    Display version.
  -T                              Disable encryption
  -d                              Create target directory, implied for file/file-pair lists
  -p                              Preserve file timestamp
  -q                              Disable progress display
  -v                              Verbose mode
(以下略)
```
