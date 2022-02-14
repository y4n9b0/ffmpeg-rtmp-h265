# 在ffmpeg中支持hevc/vp8/vp9/opus的flv格式

当前阿里云，金山云等众多cdn，已经支持hevc编码的rtmp直播。<br>
本库基于ffmpeg5.0

## rtmp codecid
hevc/vp8/vp9/opus在rtmp中的codecid没有官方协议定义，由国内众多知名cdn共同制定。
<pre>
<code>
FLV_CODECID_OPUS = 9 << FLV_AUDIO_CODECID_OFFSET

enum {
    FLV_CODECID_H263    = 2,
    FLV_CODECID_SCREEN  = 3,
    FLV_CODECID_VP6     = 4,
    FLV_CODECID_VP6A    = 5,
    FLV_CODECID_SCREEN2 = 6,
    FLV_CODECID_H264    = 7,
    FLV_CODECID_REALH263= 8,
    FLV_CODECID_MPEG4   = 9,
    FLV_CODECID_HEVC    = 12,
    FLV_CODECID_AV1     = 13,
    FLV_CODECID_VP8     = 14,
    FLV_CODECID_VP9     = 15,
};
</code>
</pre>

## 编译

下载ffmpeg源码后解压 http://ffmpeg.org/releases/ffmpeg-5.0.tar.xz<br>
把flv.h/flvdec.c/flvenc.c拷贝入libavformat文件夹中，后面ffmpeg正常编译即可。

如何编译ffmpeg，参考 
* [https://trac.ffmpeg.org/wiki/CompilationGuide](https://trac.ffmpeg.org/wiki/CompilationGuide)
* [https://github.com/runner365/srt_encoder/wiki/How-to-compile-cn#ffmpeg](https://github.com/runner365/srt_encoder/wiki/How-to-compile-cn#ffmpeg)
* [https://github.com/nldzsz/ffmpeg-build-scripts](https://github.com/nldzsz/ffmpeg-build-scripts) or [https://www.jianshu.com/p/16b14e8bb273](https://www.jianshu.com/p/16b14e8bb273)<br>

如下是我自己本地使用的命令:
```bash
export PKG_CONFIG_PATH="/usr/local/lib/pkgconfig:/usr/local/opt/openssl/lib/pkgconfig"
./configure --arch=x86_64 --enable-cross-compile --enable-avdevice --enable-doc --disable-devices --enable-ffplay --enable-ffprobe --enable-libfdk-aac --enable-libx264 --enable-libx265 --enable-libsrt --enable-nonfree --disable-asm --enable-gpl --pkgconfigdir=/usr/local/lib/pkgconfig --enable-shared
make -j 2
sudo make install
```

configure 配置详解参考 [https://blog.csdn.net/z2066411585/article/details/81239446](https://blog.csdn.net/z2066411585/article/details/81239446)<br>
一些编译错误处理参考 [https://blog.csdn.net/liwf616/article/details/99215608](https://blog.csdn.net/liwf616/article/details/99215608)

**Note** 本库的修改基于 ffmpeg 5.0，参考[ffmpeg_rtmp_h265](https://github.com/runner365/ffmpeg_rtmp_h265)(基于ffmpeg 4.1)。