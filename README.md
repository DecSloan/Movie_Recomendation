# Movie_Recomendation
**Simple program that recommends a similar movie for you to watch.**

The aim of this task is to take in a movie synopsis, compares it to other saved movie synopses to recommend a new movie based on similarity.

--

We have our sentence to compare already saved, along with the dictionary of presaved movie titles and synposes.
The function works by analysing each synopsis against the sentence to compare, rating the similarity, saving that score and then returning the movie title with the highest score.

    import math
    import spacy
    nlp = spacy.load('en_core_web_md')

    sentence_to_compare = """Will he save their world or destroy it? When the hulk becomes
    too dangerouse for the Earth, the Ilumminati trick Hulk into a shuttle and launch him 
    into space to a planet where the Hulk can live in peace. Unfortunately, Hulk lands on 
    the lanet Sakaar where he is sold into slavery nd trained as a gladiator."""

    movies = {
        "MovieA" : "When Hiccup discovers Toothless isn't the only Night Fury, he must seek 'The Hidden World', a secret Dragon Utopia before a hired tyrant named Grimmel finds it 
    first.", 
        "MovieB" : "After the death of Superman, several new people present themselves as possible successors.", 
        "MovieC" : "A darkness swirls at the center of a world-renowned dance company, one that will engulf the artistic director, an ambitious young dancer, and a grieving 
    psychotherapist. Some will succumb to the nightmare. Others will finally wake up.", 
        "MovieD" : "A humorous take on Sir Arthur Conan Doyle's classic mysteries featuring Sherlock Holmes and Doctor Watson.", 
        "MovieE" : "A 16-year-old girl and her extended family are left reeling after her calculating grandmother unveils an array of secrets on her deathbed.", 
        "MovieF" : "In the last moments of World War II, a young German soldier fighting for survival finds a Nazi captain's uniform. Impersonating an officer, the man quickly takes on 
    the monstrous identity of the perpetrators he is trying to escape from.", 
        "MovieG" : "The world at an end, a dying mother sends her young son on a quest to find the place that grants wishes.", 
        "MovieH" : "A musician helps a young singer and actress find fame, even as age and alcoholism send his own career into a downward spiral.", 
        "MovieI" : "Corporate analyst and single mom, Jen, tackles Christmas with a business-like approach until her uncle arrives with a handsome stranger in tow.", 
        "MovieJ" : "Adapted from the bestselling novel by Madeleine St John, Ladies in Black is an alluring and tender-hearted comedy drama about the lives of a group of department 
    store employees in 1959 Sydney."
    }

    sentences = list(movies.values())
    movie_title = list(movies.keys())

    model_sentence = nlp(sentence_to_compare)

    similarity_scores = []


    def most_similar_movie(sentence_to_compare, sentences):
        for sentence in sentences:
            similarity = (nlp(sentence)).similarity(model_sentence)
            similar_str = str(similarity)
            similarity_scores.append(similar_str)
        for element in similarity_scores:
            highest = max(similarity_scores)
            position = similarity_scores.index(max(similarity_scores))
        best_match = movie_title[position]
        print(f"\n{best_match} is the best match with a similarity score of {highest}")

    most_similar_movie(sentence_to_compare, sentences)
