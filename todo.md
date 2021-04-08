extend from

https://www.mongodb.com/blog/post/build-a-slack-app-in-10-minutes-with-mongodb-stitch


and extend from http://carletonatwater.com/2018/10/20/MongoDB-Stitch.html

ref:

https://gist.github.com/pca2/399bf17084b25fbfa58dc0a5c364b43d#file-weightcheck-js

exports = function(changeEvent) {
   const http = context.services.get("wt_http_service");
   const newWeight = changeEvent.fullDocument.weight;
   const thresholdWeight = 145;
   const slackURL = 'https://hooks.slack.com/services/T8M......';
   const slackMsg = `Uh-oh a weight was posted of ${newWeight}, better lay off the pie`;
    
   if(newWeight < thresholdWeight){
     return "Weight under threshold";
   } else {
     return http
       .post({ url: slackURL, body: JSON.stringify({"text": slackMsg})})
       .then(resp => {
         return resp;
       })
       .catch(err => console.log(err) );
   }
};
