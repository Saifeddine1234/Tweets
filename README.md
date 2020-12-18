# Projet–Fouille de Données
# Thème : Classification des Tweets
## Objectifs :
### • Maitriser l’API de twitter pour l’extraction des tweets
### • Maitriser la partie NLP (natural language processing) avec NLTK en Python
### • Appliquer les principes de nettoyage des données
### • Classer les tweets : regrouper ensemble les tweets qui sont similaires. C’est une étape qui peut être considérée comme une étape 
## Travail à faire
### 1- Télécharger les Tweets à partir de Twitter en utilisant l’API de twitter.
#### dans cette étape il faut extraire les données à partir des API Tweets pour cela il faut appliquer les etaps suivants :
#### a- definition des clés
CONSUMER_KEY , CONSUMER_SECRET , ACCESS_TOKEN  , ACCESS_SECRET 
#### authentication
OAuthHandler(CONSUMER_KEY, CONSUMER_SECRET)
set_access_token(ACCESS_TOKEN, ACCESS_SECRET)
#### b- Configuration l'API importer de tweet
api = tweepy.API()
#### c- stocker les tweets dans un fichier CSV
récuperer les données et stocker dans un fichier csv 
#### d- lecture de fichier 
fichierTweet = pd.read_csv('tweets.csv')
#### =>  On utilise l' API de Twitter je recuperer un tableau de 10 mill lignes et de trois columns contient des tweets de categorie differant
### 2- Utiliser la bibliothèque NLTK pour effectuer une analyse de chaque tweet et le transformer en un ensemble de mots en suivant les différentes étapes de base du processus NLP
#### a- prétraitement des données 
##### 
##### import re
##### def nettoyage(df, tweet):
#####     df[tweet] = df[tweet].str.lower()
#####     df[tweet] = df[tweet].apply(lambda x: re.sub(r"(@[A-Za-z0-9]+)|([^0-9A-Za-z \t])|(\w+:\/\/\S+)|" "|^rt|http.+?|([0-9])", "", x))
#####     return df

##### tweet_nettoyer = nettoyage(fichierTweet,'Tweet')
#### b - processus NLP
##### nlp = en_core_web_sm.load()
##### tokenizer = RegexpTokenizer(r'\w+')
##### lemmatizer = WordNetLemmatizer()
##### stop = set(stopwords.words('english'))
##### punctuation = list(string.punctuation)
##### stop.update(punctuation)
##### w_tokenizer = WhitespaceTokenizer()

##### def furnished(text):
#####     final_text = []
#####     for i in text.split():
#####         if i.lower() not in stop:
#####             word = lemmatizer.lemmatize(i)
#####             final_text.append(word.lower())
#####     return " ".join(final_text)
#### => tokenization des lignes
#### => recuperer la liste des mots en relation avec les categories choisie 
#### c- Vectoriser et standardiser les mots
##### def get_vectors(*strs):
#####    text = [t for t in strs]
#####    vectorizer = TfidfVectorizer(text)
#####    vectorizer.fit(text)
#####    return vectorizer.transform(text).toarray()
#### => recuperer la liste des mots en relation avec les categories choisie 
#### => Convertissez une collection de documents bruts en une matrice de fonctionnalités 
### d - score des categories 
#### donner un score pour chague ligne et pour chaque categorie

### 3- Utiliser l’algorithme K-Means pour classer les Tweets en k classes

#### kmeans = KMeans(n_clusters=5, init='k-means++', n_init=5, max_iter=100, random_state=0)
#### X = pivot_clusters[['politique' , 'sport']].values
#### Y_kmeans = kmeans.fit_predict(X)
#### plt.scatter(X[Y_kmeans==4, 0], X[Y_kmeans==4, 1], s=100, c='blue', label= 'Cluster ')
#### plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=100, c='black', label='Centroids' )
#### plt.title('Cluster politique - sport')
#### plt.xlabel('politique tweets')
#### plt.ylabel('sport tweets')
#### plt.legend()
#### plt.show()

