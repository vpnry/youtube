# readabletranscripts

This repo shows how to fetch the raw YouTube transcripts and use the Gemini Flash 8B API to format them.
Made by [ldenoue](https://twitter.com/ldenoue)

# How to use

open https://github.com/ldenoue/readabletranscripts and type any search term

click on the video, e.g. https://ldenoue.github.io/readabletranscripts/?id=8yzmCt0QwOQ

You will see a summary of the video and the transcript below.

# How it is done

## Breaking the transcript into chunks
We break up the raw YouTube transcript into chunks of 512 words.
We feed each chunk to Gemini with a prompt (see https://github.com/ldenoue/readabletranscripts/blob/5c51f5298f9f39bc2f35a94b84baa95fa95408bd/code.js#L410)

Notice that we send the requests in parallel to Gemini.

## Merging sentences at the boundary between 2 chunks
Once we have the formatted chunks, we now need to merge them.
For each 2 consecutive chunks `chunk1` and `chunk2`, we ask Gemini to merge the last sentence `chunk1` and the first sentence of `chunk2` (see prompt in https://github.com/ldenoue/readabletranscripts/blob/5c51f5298f9f39bc2f35a94b84baa95fa95408bd/code.js#L433)

We merge the chunks and the seams between them to obtain the final transcript.

## Linking the raw YouTube timestamps with the final transcript

In order to highlight the words as the video plays, we need to align the words from the raw YouTube transcript and the final, punctuated, transcript.

We rely on `diff.js` for that.

Now words get highlighted as the video plays, and users can also jump into the video by clicking any word in the transcript.


