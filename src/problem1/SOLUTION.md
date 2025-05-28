Provide your CLI command here:

grep '"symbol": "TSLA"' ./transaction-log.txt | awk -F'"' '{print $4}' | xargs -I {} curl -s -o ./output.txt https://example.com/api/{}


1. grep '"symbol": "TSLA"' ./transaction-log.txt: This filters lines containing TSLA.

2. awk -F'"' '{print $4}': This extracts the order_id from the filtered lines.

3. xargs -I {}: This replaces {} with each order_id in the following command.

4. curl -s -o ./output.txt https://example.com/api/{}: This sends a silent HTTP GET request to the specified URL 

and writes the output to output.txt.