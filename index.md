# K-MEANS CLUSTERING WITH MCDONALDS NUTRITION INFORMATION

Data from [kaggle](https://www.kaggle.com/mcdonalds/nutrition-facts).

Python implementation of [Lloyd's algorithm](https://en.wikipedia.org/wiki/Lloyd%27s_algorithm).

k_means.py functions are available [here](https://github.com/jherzberg/k_means_mcdonalds_nutrition/blob/master/k_means.py).

    from k_means import *

    df = pd.DataFrame.from_csv('mcdonalds_menu.csv', header=0, index_col=0)
    data = df.as_matrix(columns = ['Calories', 'Total Fat', 'Saturated Fat', 'Trans Fat', 'Cholesterol', 'Sodium', 'Carbohydrates', 'Dietary Fiber', 'Sugars', 'Protein'])

Plotting loss as a function of `k` clusters with `find_best_k(data, 20, 15)` suggests 7 clusters is optimal.


![Image of loss plot](https://github.com/jherzberg/k_means_mcdonalds_nutrition/blob/master/mcdondals_elbow_loss.png)

    # RUNS THE ALGORITHM
    centroids = get_centroids(20, 7, data)
    closest = calc_closest(data, centroids)

    # PLOTTING CLUSTERS
    x_tsne = TSNE(learning_rate =100).fit_transform(data)
    plt.scatter(x_tsne[:,0], x_tsne[:,1], c = closest)

    # SHOWS CLUSTERS
    centroids_df = pd.DataFrame(centroids, columns = ['Calories', 'Total Fat', 'Saturated Fat', 'Trans Fat', 'Cholesterol', 'Sodium', 'Carbohydrates', 'Dietary Fiber', 'Sugars', 'Protein'])
    df['Centroid'] = closest

Some results:


                                                              Serving Size  Calories  \
    Item                                                                           
    McFlurry with Oreo Cookies (Small)                 10.1 oz (285 g)       510   
    McFlurry with Oreo Cookies (Medium)                13.4 oz (381 g)       690   
    McFlurry with Oreo Cookies (Snack)                  6.7 oz (190 g)       340   
    McFlurry with Reese's Peanut Butter Cups (Medium)  14.2 oz (403 g)       810   
    McFlurry with Reese's Peanut Butter Cups (Snack)    7.1 oz (202 g)       410   

                                                       Protein  Centroid  
    Item                                                                  
    McFlurry with Oreo Cookies (Small)                      12         1  
    McFlurry with Oreo Cookies (Medium)                     15         4  
    McFlurry with Oreo Cookies (Snack)                       8         1  
    McFlurry with Reese's Peanut Butter Cups (Medium)       21         4  
    McFlurry with Reese's Peanut Butter Cups (Snack)        10         1

T-SNE plot:

![image of t_sne plot](https://github.com/jherzberg/k_means_mcdonalds_nutrition/blob/master/mcdondalds_t_sne.png)

### Josh Herzberg
