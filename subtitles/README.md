# Generate subtitles for ZAP Videos using whisper

Here is a short guide on how the subtitles were created using OpenAI's Whisper.
**A Nvidia graphics card with Cuda cores is required (The absolute minimum is the Nvidia 1080Ti).** The more VRAM the better, as larger models can then be used if necessary. In addition to Whisper, you also need an audio file, e.g. in .mp3 format, which you want to transcribe.

## Video download

Regardless of the project, you first need the video file to create the audio file (see next step). 
There are many tools and online services out there - one way to do this quickly and easily is [JDownloader](https://jdownloader.org/download/index?s=lng_en). 
After installation, simply start the program, copy the YouTube link and import it into JDownloader. It may be that ffmpeg needs to be installed. Then just select the video file and click on "Next". The download will now start in the quality provided by the uploader.

## The audio file

To be able to use Whisper, you need the audio part of the video. First you have to download the video with the tool of your choice. Then you have to cut off the video or audio part. You can use [DaVinci Resolve](https://www.blackmagicdesign.com/products/davinciresolve) as a free and well-known tool. The recommended audio format is .mp3.

## Install Whisper

First you have to install Whisper - you can find out how to do this in the official repository [Whisper](https://github.com/openai/whisper). Here you will also find a list of the requirements, languages and possibilities of what you can do with it.

## Generate .srt file from the audio file

For Whisper to work at all, there must be **no spaces** in the file name of the audio file.

Here is an example - the language is important if you know which language is used in the audio file - otherwise omit this entry and it will be 
recognized automatically. For the model, please note that you should use the one that does not exceed the VRAM of the graphics card. Always use the largest possible model for you. For everything else, please refer to Whisper's instructions.

    whisper .\audiofile.mp3 --language English --model large --task transcribe --output_format srt --output_dir YOUR OUTPUT DIRECTORY
    

With a 1080Ti, the transcript for a 30 minute video takes about 45 minutes.

## The follow-up check

Once the .srt file has been successfully created, you should always check the content again. Notepad++, VSCode etc. are recommended for editing the file. In the release version v20231117 Whisper tends to hallucinate. This creates incorrect sentences, punctuation or invented words. In addition, Whisper sometimes has difficulties recognizing special names, first names and surnames. You may have to correct this manually.

> [!TIP]
> If you have a section where hallucinations have taken place, it is sufficient to just delete the text. You do not need to change the consecutive number of the subtitle or the time stamp. YouTube, for example, recognizes these gaps and skips these lines when importing. This saves you a lot of work.