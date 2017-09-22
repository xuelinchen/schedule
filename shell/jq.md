# install jq
	apt install jq -y

# jq --help
	jq - commandline JSON processor [version 1.5-1-a5b5cbe]
	Usage: jq [options] <jq filter> [file...]
	
	        jq is a tool for processing JSON inputs, applying the
	        given filter to its JSON text inputs and producing the
	        filter's results as JSON on standard output.
	        The simplest filter is ., which is the identity filter,
	        copying jq's input to its output unmodified (except for
	        formatting).
	        For more advanced filters see the jq(1) manpage ("man jq")
	        and/or https://stedolan.github.io/jq
	
	        Some of the options include:
	         -c             compact instead of pretty-printed output;
	         -n             use `null` as the single input value;
	         -e             set the exit status code based on the output;
	         -s             read (slurp) all inputs into an array; apply filter to it;
	         -r             output raw strings, not JSON texts;
	         -R             read raw strings, not JSON texts;
	         -C             colorize JSON;
	         -M             monochrome (don't colorize JSON);
	         -S             sort keys of objects on output;
	         --tab  use tabs for indentation;
	         --arg a v      set variable $a to value <v>;
	         --argjson a v  set variable $a to JSON value <v>;
	         --slurpfile a f        set variable $a to an array of JSON texts read from <f>;
	        See the manpage for more options.
	        
# example
	1. get value
		echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".status"
		0
		echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".info" | sed 's/"//g'
		we are success
		echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".data.client.client_id" | sed 's/"//g'
		123456
	2. filter data
		echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq '.data|.client'
		{
		  "client_id": "123456",
		  "client_secret": "567890"
		}
		