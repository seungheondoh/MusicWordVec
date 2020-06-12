<p align="justify">
In this work, we investigate various word embedding spaces trained with different combinations of general text data and music-specific text data to connect listening contexts to songs in a more balanced manner. 
</p>

### Overview
<p align="justify">
Music listeners often rely on various listening contexts such as mood, theme, time, location and activity to find songs. This can be handled by defining a dictionary of contextual terms and directly associating them with songs as a class label. However, this music tagging approach (i.e., multi-label classification) is highly limited in embracing all possible contextual expressions that listeners can use as a natural language. For example, a listener may use 'club' to search electronic dance music. Unless the model is trained with the specific word, it is not possible to take it as a query. This issue has been addressed by representing the tag words with embedding vectors and associating them with songs in several different settings, for example, zero-shot learning, query-by-blending and multi-task music representation learning. They used the word embedding trained with either general text (e.g., Wikipedia or Gigaword) or music-specific corpus (e.g., tags, lyrics, artist IDs, track IDs). However, the general text may not reflect musical aspects, whereas music-specific corpus may not incorporate various listening contexts which are not directly related to music and also the size of vocabulary can be limited. 
</p>

![Model Architecture Ver 5 small artboard 2](./assets/img/figure1.png)
<p align="center">Figure.1 Train W2V and T-sne Visualization</p>

### Results
<p align="justify">

The t-SNE plot in Figure 1 provides a more intuitive  example on the result. We used two music genre terms 'electronic' and 'house' and three listening context terms 'club', 'club_dance', and 'partying'. In Wikipedia, they spread apart having only 'house' and 'club' close together. In the music corpus, the two genre terms and 'club' and 'club_dance' are tightly clustered while having 'partying' away. In the music corpus with Wikipedia, the context term 'partying' also becomes closer to the two genres and other context terms. This indicates that using both general and music-specific data provides more balanced correlation between music and listening context.
</p>
|                               Corpus                              |  Size | Unique  Word | Unique  Track | Unique  Artist | AllMusic (Seen) |       | LastFm (Unseen) |       |
|:-----------------------------------------------------------------:|:-----:|:------------:|:-------------:|:--------------:|:---------------:|-------|-----------------|-------|
|                                                                   |       |              |               |                |    spearmanr    |  nDCG |    spearmanr    |  nDCG |
| [AllMusic Tags   + Amazon Music Reviews] (Augmented) + Wikipedia  | 1.98B |   11622471   |     521778    |      28330     |      0.194      | 0.490 |      0.312      | 0.643 |
|         AllMusic Tags + Amazon Music Reviews +   Wikipedia        |  1.8B |   11622471   |     521778    |      28330     |      0.187      | 0.418 |      0.226      | 0.599 |
|                    AllMusic Tags   + Wikipedia                    | 1.76B |   11163229   |     507435    |      25203     |      0.157      | 0.402 |      0.183      | 0.589 |
|        [AllMusic Tags   + Amazon Music Reviews] (Augmented)       | 0.27B |    664163    |     521778    |      28330     |      0.267      | 0.473 |      0.407      | 0.681 |
|                AllMusic Tags + Amazon Music Reviews               | 45.3m |    664163    |     521778    |      28330     |      0.187      | 0.398 |      0.358      | 0.670 |
|                           AllMusic Tags                           |  7.1m |     1401     |     507435    |      25203     |      0.252      | 0.409 |                 |       |
|                             Wikipedia                             | 1.75B |   11163055   |       0       |        0       |      0.098      | 0.356 |      0.162      | 0.600 |

### Retrieval Result

<script>
function pauseOthers(ele) {
    $("audio").not(ele).each(function (index, audio) {audio.pause();});
}
</script>

<style>
.main-content table {
    display: inline-table;
}
table {
    table-layout:fixed;
    width: 100%;
    overflow: hidden;
}
#player{
    width: 100%;
}
</style>

<table>
    <tr>
        <th> Query </th>
        <th> Similar Song 1 </th>
        <th> Similar Song 2 </th>
        <th> Similar Song 3 </th>
    </tr>
    <tr>
        <th> club </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> club,house,<br/> electronic</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_house_electornic/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> club,electronic,<br/> summer</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/club_electronic_summer/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> happy,jazz,cafe </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/happy_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> sad,jazz,cafe </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/sad_jazz_cafe/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> energetic,rap, <br/> exercise_workout</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_rap_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> energetic,pop_rock,<br/> excercise_workout </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/energetic_pop_rock_exercise_workout/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> forest,ambient</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_ambient/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
    <tr>
        <th> forest,soundtrack</th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank0.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank1.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/forest_soundtrack/rank2.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>