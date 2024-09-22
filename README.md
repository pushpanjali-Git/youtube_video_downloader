# youtube_video_downloader
youtube video downloader using django


<!DOCTYPE html> 
<html> 
<body> 

<h1>Youtube video downloader</h1> 


<form action="" method="post"> 
{% csrf_token %} 

<label for="link">Enter URL:</label> 
<input type="text" id="link" name="link"><br><br> 
<input type="submit" value="Submit"> 
</form> 

</body> 
</html>

# # importing all the required modules 
from django.shortcuts import render, redirect 
from pytube import *


# defining function 
def youtube(request): 

	# checking whether request.method is post or not 
	if request.method == 'POST': 
		
		# getting link from frontend 
		link = request.POST['link'] 
		video = YouTube(link) 

		# setting video resolution 
		stream = video.streams.get_lowest_resolution() 
		
		# downloads video 
		stream.download() 

		# returning HTML page 
		return render(request, 'youtube.html') 
	return render(request, 'youtube.html')

