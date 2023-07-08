<!DOCTYPE html>
<html>
<head>
  <title>My Blog Editor</title>
  <style>
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
    }

    input[type="text"],
    textarea {
      width: 100%;
      margin-bottom: 10px;
    }

    button {
      display: block;
      margin-top: 10px;
    }

    .post {
      margin-bottom: 20px;
      padding: 10px;
      border: 1px solid #ccc;
    }

    .post h2 {
      margin-top: 0;
    }

    .post p {
      margin-bottom: 10px;
    }

    .post img,
    .post video {
      max-width: 100%;
    }

    .file-upload-wrapper {
      position: relative;
      overflow: hidden;
      display: inline-block;
    }

    .file-upload-wrapper input[type="file"] {
      font-size: 100px;
      position: absolute;
      left: 0;
      top: 0;
      opacity: 0;
      cursor: pointer;
    }

    .file-upload-wrapper label {
      display: block;
      padding: 10px 20px;
      background-color: #e9e9e9;
      color: #555;
      cursor: pointer;
    }

    .file-upload-wrapper span {
      display: inline-block;
      margin-top: 8px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>My Blog Editor</h1>
    <form id="blogForm">
      <label for="title">Title:</label>
      <input type="text" id="title" name="title">
      <label for="content">Content:</label>
      <textarea id="content" name="content"></textarea>
      <div class="file-upload-wrapper">
        <label for="image" class="file-upload">
          Select Image
          <span id="image-name"></span>
        </label>
        <input type="file" id="image" name="image" accept="image/*" onchange="updateFileName('image')">
      </div>
      <div class="file-upload-wrapper">
        <label for="video" class="file-upload">
          Select Video
          <span id="video-name"></span>
        </label>
        <input type="file" id="video" name="video" accept="video/*" onchange="updateFileName('video')">
      </div>
      <button type="button" onclick="addPost()">Add Post</button>
    </form>
    <div id="blogPosts"></div>
  </div>

  <script>
    function addPost() {
      var title = document.getElementById("title").value;
      var content = document.getElementById("content").value;
      var imageFile = document.getElementById("image").files[0];
      var videoFile = document.getElementById("video").files[0];

      // Create a new blog post element
      var post = document.createElement("div");
      post.classList.add("post");

      // Add the post title
      var postTitle = document.createElement("h2");
      postTitle.innerText = title;
      post.appendChild(postTitle);

      // Add the post content
      var postContent = document.createElement("p");
      postContent.innerText = content;
      post.appendChild(postContent);

      // Add the post image
      if (imageFile) {
        var postImage = document.createElement("img");
        postImage.classList.add("post-image");
        post.appendChild(postImage);

        var reader = new FileReader();
        reader.onload = function (event) {
          postImage.src = event.target.result;
        };
        reader.readAsDataURL(imageFile);
      }

      // Add the post video
      if (videoFile) {
        var postVideo = document.createElement("video");
        postVideo.classList.add("post-video");
        postVideo.controls = true;
        post.appendChild(postVideo);

        var reader = new FileReader();
        reader.onload = function (event) {
          postVideo.src = event.target.result;
        };
        reader.readAsDataURL(videoFile);
      }

      // Append the post to the blogPosts container
      var blogPosts = document.getElementById("blogPosts");
      blogPosts.appendChild(post);

      // Clear the form inputs
      document.getElementById("title").value = "";
      document.getElementById("content").value = "";
      document.getElementById("image").value = "";
      document.getElementById("video").value = "";
      document.getElementById("image-name").innerText = "";
      document.getElementById("video-name").innerText = "";
    }

    function updateFileName(inputId) {
      var fileName = document.getElementById(inputId).files[0].name;
      document.getElementById(inputId + "-name").innerText = fileName;
    }
  </script>
</body>
</html>
