# 参考サイト https://qiita.com/nontan18/items/579daf033a4644f2285a

FROM alpine:3.9.4
LABEL maintainer="c011610353@edu.teu.ac.jp"

RUN apk update \
&&  apk add perl wget fontconfig-dev xz tar vim 
ADD http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz /tmp/install-tl-unx.tar.gz 
RUN  mkdir /tmp/install-tl-unx \ 
&& tar -xvf /tmp/install-tl-unx.tar.gz -C /tmp/install-tl-unx --strip-components=1 \
&& echo "selected_scheme scheme-basic" >> /tmp/install-tl-unx/texlive.profile \ 
&& /tmp/install-tl-unx/install-tl -profile /tmp/install-tl-unx/texlive.profile \
&& TEX_LIVE_VERSION=$(/tmp/install-tl-unx/install-tl --version | tail -n +2 | awk '{print $5}'); \
    ln -s "/usr/local/texlive/${TEX_LIVE_VERSION}" /usr/local/texlive/latest 
ENV PATH="/usr/local/texlive/latest/bin/x86_64-linuxmusl:${PATH}"
RUN mkdir /texsrc \
&& tlmgr init-usertree \
&& tlmgr update --all --self \ 
&& tlmgr install collection-latexrecommended collection-latexextra xetex latexmk multirow collection-langjapanese collection-fontsrecommended collection-fontutils fontawesome  \
&& wget https://osdn.net/projects/mytexpert/downloads/26068/jlisting.sty.bz2 \
&& bzip2 -d jlisting.sty.bz2 \
&& cp -p jlisting.sty /usr/local/texlive/2019/texmf-dist/tex/latex/listings/ \
&& mktexlsr  
COPY ./.latexmkrc /root/.latexmkrc

VOLUME /texsrc

WORKDIR /texsrc

