FROM rocker/shiny


# Guided by Shiny tutorials and https://github.com/flaviobarros/shiny-wordcloud/blob/master/Dockerfile


MAINTAINER Brian O'Meara <omeara.brian@gmail.com>
RUN \
rm -rf /var/lib/apt/lists/* && \
apt-get update && \
apt-get -y dist-upgrade && \
apt-get install -y software-properties-common && \
apt-get install -y libssl-dev  && \
apt-get install -y libxml2-dev && \
apt-get install -y libprotobuf-dev && \
apt-get install -y protobuf-compiler && \
apt-get install -y php libapache2-mod-php php-cli && \
apt-get install -y git-core && \
apt-get install -y wget && \
echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" > ~/.Rprofile && \
Rscript -e "install.packages('devtools')" && \
Rscript -e "install.packages('strap')" && \
Rscript -e "devtools::install_github('phylotastic/datelife')" && \
mkdir /usr/local/pathd8download && \
wget http://www2.math.su.se/PATHd8/PATHd8.zip -O /usr/local/pathd8download/PATHd8.zip && \
cd /usr/local/pathd8download && \
unzip /usr/local/pathd8download/PATHd8.zip && \
cc PATHd8.c -O3 -lm -o PATHd8 && \
cp PATHd8 /usr/local/bin/PATHd8
RUN \
cd /srv && \
rm -r /srv/shiny-server/* && \
git clone https://github.com/bomeara/brianomearaorg.git && \
mv /srv/brianomearaorg/web/* /srv/shiny-server/
EXPOSE 80
CMD ["/usr/bin/shiny-server.sh"]
