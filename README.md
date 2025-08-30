# error-handling in shell scripting 
# I learnt about the concept of error handling in shell scripting on how it is important to catch error early during development stage and i learnt the use of conditional statement to cache and check this errors if they occurs and u should always anticipate for errors so u think of the most kinds of errors in your development and when it occurs there should be a display message of the type of errors that occured during developmet. 
# here is a error handling function for s3 bucket
# Function to create S3 buckets for different departments
# create_s3_buckets() {"\n    company=\"datawise\"\n    departments=(\"Marketing\" \"Sales\" \"HR\" \"Operations\" \"Media\")\n    \n    for department in \"${departments[@]"}"; do
        bucket_name="${company}-${department}-Data-Bucket"
        
        # Check if the bucket already exists
        if aws s3api head-bucket --bucket "$bucket_name" &>/dev/null; then
            echo "S3 bucket '$bucket_name' already exists."
        else
            # Create S3 bucket using AWS CLI
            aws s3api create-bucket --bucket "$bucket_name" --region your-region
            if [ $? -eq 0 ]; then
                echo "S3 bucket '$bucket_name' created successfully."
            else
                echo "Failed to create S3 bucket '$bucket_name'."
            fi
        fi
    done
}
# use aws s3api head-bucket to check if the bucket already exist 
# then run a conditinoal ifelse statement to be sure and produce a feedback 
# this checks for if the bucket exist then display a message if it already exist 
# also check for errors if its created successfully if it failed it will display a message saying failed to create s3 bucket
