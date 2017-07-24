# K-MEANS CLUSTERING WITH MCDONALDS NUTRITION INFORMATION

Data from [kaggle](https://www.kaggle.com/mcdonalds/nutrition-facts).

Python implementation of [Lloyd's algorithm](https://en.wikipedia.org/wiki/Lloyd%27s_algorithm).

k_means.py functions are available [here](https://github.com/jherzberg/k_means_mcdonalds_nutrition/blob/master/k_means.py).
    
    from k_means import *

    df = pd.DataFrame.from_csv('mcdonalds_menu.csv', header=0, index_col=0)
    data = df.as_matrix(columns = ['Calories', 'Total Fat', 'Saturated Fat', 'Trans Fat', 'Cholesterol', 'Sodium', 'Carbohydrates', 'Dietary Fiber', 'Sugars', 'Protein'])

Plotting loss as a function of `k` clusters with `find_best_k(data, 20, 15)` suggests 7 clusters is optimal.

![Image of loss plot]
(https://github.com/jherzberg/k_means_mcdonalds_nutrition/blob/master/mcdondals_elbow_loss.png)
    
    # RUNS THE ALGORITHM
    centroids = get_centroids(20, 7, data)
    closest = calc_closest(data, centroids)

    # PLOTTING CLUSTERS
    x_tsne = TSNE(learning_rate =100).fit_transform(data)
    plt.scatter(x_tsne[:,0], x_tsne[:,1], c = closest)

    # SHOWS CLUSTERS
    centroids_df = pd.DataFrame(centroids, columns = ['Calories', 'Total Fat', 'Saturated Fat', 'Trans Fat', 'Cholesterol', 'Sodium', 'Carbohydrates', 'Dietary Fiber', 'Sugars', 'Protein'])
    df['centroid'] = closest

Some results: `df.tail()`.

                                                              Serving Size  Calories  \
    Item                                                                           
    McFlurry with Oreo Cookies (Small)                 10.1 oz (285 g)       510   
    McFlurry with Oreo Cookies (Medium)                13.4 oz (381 g)       690   
    McFlurry with Oreo Cookies (Snack)                  6.7 oz (190 g)       340   
    McFlurry with Reese's Peanut Butter Cups (Medium)  14.2 oz (403 g)       810   
    McFlurry with Reese's Peanut Butter Cups (Snack)    7.1 oz (202 g)       410   

                                                       Calories from Fat  \
    Item                                                                   
    McFlurry with Oreo Cookies (Small)                               150   
    McFlurry with Oreo Cookies (Medium)                              200   
    McFlurry with Oreo Cookies (Snack)                               100   
    McFlurry with Reese's Peanut Butter Cups (Medium)                290   
    McFlurry with Reese's Peanut Butter Cups (Snack)                 150   

                                                       Total Fat  Saturated Fat  \
    Item                                                                          
    McFlurry with Oreo Cookies (Small)                      17.0            9.0   
    McFlurry with Oreo Cookies (Medium)                     23.0           12.0   
    McFlurry with Oreo Cookies (Snack)                      11.0            6.0   
    McFlurry with Reese's Peanut Butter Cups (Medium)       32.0           15.0   
    McFlurry with Reese's Peanut Butter Cups (Snack)        16.0            8.0   

                                                       Trans Fat  Cholesterol  \
    Item                                                                        
    McFlurry with Oreo Cookies (Small)                       0.5           45   
    McFlurry with Oreo Cookies (Medium)                      1.0           55   
    McFlurry with Oreo Cookies (Snack)                       0.0           30   
    McFlurry with Reese's Peanut Butter Cups (Medium)        1.0           60   
    McFlurry with Reese's Peanut Butter Cups (Snack)         0.0           30   

                                                       Sodium  Carbohydrates  \
    Item                                                                       
    McFlurry with Oreo Cookies (Small)                    280             80   
    McFlurry with Oreo Cookies (Medium)                   380            106   
    McFlurry with Oreo Cookies (Snack)                    190             53   
    McFlurry with Reese's Peanut Butter Cups (Medium)     400            114   
    McFlurry with Reese's Peanut Butter Cups (Snack)      200             57   

                                                       Dietary Fiber  Sugars  \
    Item                                                                       
    McFlurry with Oreo Cookies (Small)                             1      64   
    McFlurry with Oreo Cookies (Medium)                            1      85   
    McFlurry with Oreo Cookies (Snack)                             1      43   
    McFlurry with Reese's Peanut Butter Cups (Medium)              2     103   
    McFlurry with Reese's Peanut Butter Cups (Snack)               1      51   

                                                       Protein  centroid  
    Item                                                                  
    McFlurry with Oreo Cookies (Small)                      12         1  
    McFlurry with Oreo Cookies (Medium)                     15         4  
    McFlurry with Oreo Cookies (Snack)                       8         1  
    McFlurry with Reese's Peanut Butter Cups (Medium)       21         4  
    McFlurry with Reese's Peanut Butter Cups (Snack)        10         1
