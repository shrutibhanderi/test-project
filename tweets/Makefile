all: download prep analyze

download:
	mkdir data
	chmod -R 777 /Users/shrutibhanderi/Desktop/gittutorial/test-project/tweets/data
	sudo wget www.derekruths.com/static/reading_tweets/books_tweets100000.txt.gz -P /Users/shrutibhanderi/Desktop/gittutorial/test-project/tweets/data
prep:
	gzip -d data/books_tweets100000.txt.gz
	jq -r '[.userid,.created_at,.lang,.text] | @tsv' data/books_tweets100000.txt > book_tweets.tsv
	awk '$$2 ~ /Oct/ && $$3 ~/23/ && $6$~ /2012/ {print }' book_tweets.tsv > tweetsOct2012.tsv
	sed -n '/#gameofthrones/p' book_tweets.tsv >tweets_got.tsv
analyze:
	touch results.txt
	@echo "How many tweets have Russian language?" > results.txt
	grep '"lang":"ru"' data/books_tweets100000.txt | wc -l >> results.txt	
	@echo "How many tweets are from August 2016?" >> results.txt	
	sed -n '/Aug.*2016/p' data/books_tweets100000.txt | wc -l >> results.txt
	@echo "How many tweets contain a retweet?" >> results.txt
	sed -n '/RT.*/p' data/books_tweets100000.txt | wc -l >> results.txt
	@echo "How many tweets mention gameofthrones?" >> results.txt
	sed -n '/#gameofthrones/p' data/books_tweets100000.txt | wc -l >> results.txt
