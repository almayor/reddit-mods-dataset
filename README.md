# RedditMods: Moderators of top-25'000 subreddits
<a href="https://www.kaggle.com/datasets/gingerbadger/redditmods-moderators-of-top-25k-subreddits/data" rel="Kaggle dataset">![Kaggle](https://img.shields.io/badge/Kaggle-035a7d?style=for-the-badge&logo=kaggle&logoColor=white)</a> ![Reddit](https://img.shields.io/badge/Reddit-%23FF4500.svg?style=for-the-badge&logo=Reddit&logoColor=white)

_RedditMods_ is a dataset that lists moderators of 25'834 largest and most popular communities on Reddit. The dataset is ideal for studying subreddits as a graph, where edges are moderators and nodes are subreddits.

## Data Collection

The data was scraped in the associated [Jupyter Notebook](code/reddit-mods-ds.ipynb). The data was publically available and collected on 06 Feb 2024. All usernames were anonymised by hashing with SHA256, so that they cannot be linked to the moderators' Reddit accounts.

## Description of Files

The data is available both as a table and a bipartite graph.

#### GEXF – data in graph format

1. `graph.gexf`

	A bipartite graph, where nodes in the first group (having attribute `bipartite=0`) are moderators and nodes in the second group (having attribute `bipartite=1`) are subreddits. A moderator-node is connected with a subreddit-node if that moderator moderates this subreddit.
	
	Tags:
	* `size` on subreddit-nodes, indicating the number of subreddit's members
	  
	<hr>
	
#### CSV – data in table format

1. `subreddits.csv`

	Contains 25K subreddits from [Reddit's Top](www.reddit.com/best/communities/1/), combined with the [list](http://www.reddit.com/subreddits/) of Reddit's most popular communities. The two lists are not identical, as described in the [Jupyter notebook](code/reddit-mods-ds.ipynb). The headers are:

	* `name`: Name of subreddit
	* `n_members`: Number of members
	
	<hr>
	
2. `moderators.csv`

	Each row describes a subreddit-moderator pair:
	
	* `subreddit`: Name of subreddit
	* `moderator`: Username of moderator (anonymised by hashing)
	
	<hr>

3. `bots.csv`
	List of moderators that were identified as bots  by the primitive procedure, described in the previous section. These accounts were already removed from `moderators.csv`.
	
	* `name`: Username of bot

	<hr>

## Examples

* [Visualising a cluster of subreddits moderated by a group of users](./example/example.ipynb)

## Notes and warnings

I used a very simple procedure to filter out auto-moderators: (1) a short list of known bots (e.g. `u/AutoModerator`), (2) username starts or ends with `bot`. An additional procedure to identify and remove bots might be necessary. For an example, see [this notebook](example/example.ipynb).
