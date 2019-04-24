# auction-api
An Auction Management REST API

TASK ONE->API to list all items on auction, upcoming auctions, previous auctions
	http://localhost:8080/auction/items ---- will give the list of all items in auction_items table, since all items auctioned before or going to be auctioned
									 are present in auction_items table
									 
TASK TWO->API to list details of an item.
			SUBTASK ONE -> If the item is already auctioned should give the details of buyer and the amount
				http://localhost:8080/auction/items/<ITEM_ID> will give user details when auction has ended and winner is there
			SUBTASK TWO -> If the item is currently in auction, should list the highest bid amount
				http://localhost:8080/auction/items/<ITEM_ID> will give maximum BID amount if auction is still ON 
				(HAVE MADE NULL FOR ITEM_ID=6 FOR TESTING)
				
TASK THREE->Will be running the cron job at the starting of every minute to check if end time of auction of any item has reached or not,
			if yes it performs the updation on auction_items table, expression for the cron job to run daily at midnight will be 0 * * * * *
				->first we get the list of all items in auction_items table
				->go through each and every item one by one
				->if for any entry in table, we have current timestamp greater than or equal to the end time, we get that item id, 
				lookup for user with maximum bid in BIDS table, get the proper user instance from users table and update it in auction_items table
				->SECOND PART OF SCHEDULED TASK --- SENDING MAIL IS IN PROGRESS
TASK FOUR->Submitting new bids
			->URI for that will be http://localhost:8080/auction/bids/add
			->ADDING AUTHENTICATION TO THIS URI WAS IN PROGRESS AS WELL
				
TASK FIVE->View all bids submitted by an authenticated user
		Since, we are going to view the BIDS submitted by a user, we will be using below URI,
			http://localhost:8080/auction/bids/<USER_ID>
			Above URI will display the item name against which bid has been placed AND the BIDDING AMOUNT
			NULL RESPONSE IF USER_ID WHICH DOES NOT EXIST IS PROVIDED