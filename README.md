# RedditMods: Moderators of top-25'000 subreddits
<a href="https://www.kaggle.com/datasets/gingerbadger/redditmods-moderators-of-top-25000-subreddits" rel="Kaggle dataset">![Kaggle](https://img.shields.io/badge/Kaggle-035a7d?style=for-the-badge&logo=kaggle&logoColor=white)</a> ![Reddit](https://img.shields.io/badge/Reddit-%23FF4500.svg?style=for-the-badge&logo=Reddit&logoColor=white)

_RedditMods_ is a dataset that lists moderators of 25'834 largest and most popular communities on Reddit. It's ideal for studying subreddits as a graph, where edges are moderators and nodes are subreddits.

## Data Collection

The data was scraped in the associated [Jupyter Notebook](code/reddit-mods-db.ipynb). All data was collected on 06 Feb 2024.

## Description of Files

#### CSV – data in table format

1. `subreddits.csv`

	Contains 25K subreddits from [Reddit's Top](www.reddit.com/best/communities/1/), combined with the [list](http://www.reddit.com/subreddits/) of Reddit's most popular communities. The two lists are not identical, as described in the Jupyter notebook. The headers are:

	* `name`: Name of subreddit
	* `n_members`: Number of members
	
	<hr>
	
2. `moderators.csv`

	Each row describes a subreddit-moderator pair:
	
	* `subreddit`: Name of subreddit
	* `moderator`: Username of moderator
	
	I used a very simple procedure to filter out auto-moderators: (1) a short list of known bots (e.g. `u/AutoModerator`), (2) username starts or ends with `bot`.
	
	*Important:* An additional procedure to identify and remove bots might be necessary. For example, one could remove all accounts that moderate >100 communities.
	<hr>

3. `bots.csv`
	List of moderators that were identified as bots  by the primitive procedure, described in the previous section. These accounts were already removed from `moderators.csv`.
	
	* `name`: Username of bot

	<hr>

#### GEXF – data in graph format

1. `multi_graph.gexf`

	  A multigraph where nodes are subreddits and edges are moderators. Both nodes and edges carry labels. A pair of nodes is connected by an edge, if the associated subreddits have a moderator in common. If they share two or more moderators, they will be connected by multiple edges. 
	<hr>
	
2. `simple_graph.gexf`

	A multigraph where nodes are subreddits and edges are moderators. Unlike `multi_graph.gexf`, here a pair of subreddits is connected by at most a single edge. Each edge carries an addition property, called `weight`, which reflected how many moderators there are in common. An edge label is a list of all moderators in common, separated by commas. 
  
  	It is useful because programs, such as GePhi, don't support multigraphs.
  
	<hr>


## Examples

* [Visualising a cluster of subreddits moderated by a group of users](./example)
