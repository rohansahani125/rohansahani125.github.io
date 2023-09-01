# Welcome to my webpage
# the webpage is underprocess



<!DOCTYPE html>
<html>
<head>
    <title>Instagram Video Downloader</title>
</head>
<body>
    <h1>Instagram Video Downloader</h1>
    <input type="text" id="urlInput" placeholder="Enter Instagram video URL">
    <button onclick="downloadVideo()">Download</button>
    <p id="downloadLink"></p>

    <script>
        function downloadVideo() {
            var url = document.getElementById('urlInput').value;
            var videoId = extractVideoId(url);
            if (videoId) {
                var downloadLink = 'https://www.instagram.com/p/' + videoId + '/?__a=1';
                fetch(downloadLink)
                    .then(response => response.json())
                    .then(data => {
                        var videoUrl = data.graphql.shortcode_media.video_url;
                        var linkElement = document.getElementById('downloadLink');
                        linkElement.innerHTML = '<a href="' + videoUrl + '" download>Download Video</a>';
                    })
                    .catch(error => {
                        console.error(error);
                        alert('An error occurred while fetching the video.');
                    });
            } else {
                alert('Invalid Instagram URL');
            }
        }

        function extractVideoId(url) {
            var regex = /\/p\/([^/]+)\//;
            var match = url.match(regex);
            return match ? match[1] : null;
        }
    </script>
</body>
</html>
