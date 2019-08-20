FROM ubuntu:latest

RUN apt-get update && \
	apt-get install -y libx11-6 libfreetype6 libxrender1 libfontconfig1 libxext6 xvfb curl bzip2 unzip python3 python3-pip git zip && \
	pip3 install nrfutil

RUN Xvfb :1 -screen 0 1024x768x16 &

RUN curl -X POST -F "fileid=8F19D314130548209E75EFFADD9348DB" https://www.nordicsemi.com/api/sitecore/Products/DownloadPlatform -o nrftools.tar && \
	tar -xvf nrftools.tar && \
	rm nrftools.tar
RUN curl -L https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2019q3/RC1.1/gcc-arm-none-eabi-8-2019-q3-update-linux.tar.bz2?revision=c34d758a-be0c-476e-a2de-af8c6e16a8a2?product=GNU%20Arm%20Embedded%20Toolchain,64-bit,,Linux,8-2019-q3-update -o gcc-arm-none-eabi-8-2019-q3-update-linux.tar.bz2 && \
	tar -xvjf gcc-arm-none-eabi-8-2019-q3-update-linux.tar.bz2 && rm gcc-arm-none-eabi-8-2019-q3-update-linux.tar.bz2 
ENV PATH="/gcc-arm-none-eabi-8-2019-q3-update-linux/bin:/mergehex:/nrfjprog:$PATH"


RUN curl https://www.segger.com/downloads/embedded-studio/Setup_EmbeddedStudio_ARM_v350_linux_x64.tar.gz -o ses.tar.gz && \
	tar -zxvf ses.tar.gz && \
	DISPLAY=:1 $(find arm_segger_* -name "install_segger*") --copy-files-to /ses && \
	rm ses.tar.gz && \
	rm -rf arm_segger_embedded_studio_*

RUN curl https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v15.x.x/nRF5_SDK_15.2.0_9412b96.zip -o nRF5_SDK_15.2.0_9412b96.zip && unzip nRF5_SDK_15.2.0_9412b96.zip && rm nRF5_SDK_15.2.0_9412b96.zip

CMD ["/ses/bin/emBuild"]
