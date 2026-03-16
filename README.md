# Netflix-Data-Analysis
My mini pet project
    {
      "cell_type": "markdown",
      "source": [
        "Actors and Actress who have given most Number of Movies\n",
        "\n",
        "Актеры и актрисы, снявшиеся в наибольшем количестве фильмов\n",
        "*  Фильтруем только фильмы и убираем строки, где актеры не указаны\n",
        "*  Разделяем имена (из строки в список) и превращаем список в отдельные строки (explode)\n",
        "\n",
        "\n"
      ],
      "metadata": {
        "id": "GQ1ZNdtfexA0"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "# Фильтруем только фильмы и убираем строки, где актеры не указаны\n",
        "movies = df[df['type'] == 'Movie'].dropna(subset=['cast'])\n",
        "\n",
        "# Разделяем имена и превращаем список в отдельные строки\n",
        "top_actors = movies['cast'].str.split(', ').explode().value_counts()\n",
        "\n",
        "print(\"Актеры с наибольшим количеством фильмов на Netflix:\")\n",
        "print(top_actors.head(10))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "PWysT3yXF8ot",
        "outputId": "d24dd6e3-ace9-4b03-f224-471b1ff4505d"
      },
      "execution_count": 20,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Актеры с наибольшим количеством фильмов на Netflix:\n",
            "cast\n",
            "Anupam Kher         42\n",
            "Shah Rukh Khan      35\n",
            "Naseeruddin Shah    32\n",
            "Akshay Kumar        30\n",
            "Om Puri             30\n",
            "Paresh Rawal        28\n",
            "Julie Tejwani       28\n",
            "Amitabh Bachchan    28\n",
            "Boman Irani         27\n",
            "Rupa Bhimani        27\n",
            "Name: count, dtype: int64\n"
          ]
        }
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "Find out which types of genre has most movies and TV Shows\n",
        "\n",
        "К каким жанрам относится большинство фильмов и телешоу"
      ],
      "metadata": {
        "id": "7ClTaf1Vsaco"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "def get_top_genres(data_type):\n",
        "    filtered_df = df[df['type'] == data_type].dropna(subset=['listed_in'])\n",
        "    genres = filtered_df['listed_in'].str.split(', ').explode()\n",
        "\n",
        "    return genres.value_counts().head(5)\n",
        "\n",
        "print(\"САМЫЕ ПОПУЛЯРНЫЕ ЖАНРЫ НА NETFLIX\")\n",
        "print(\"-\" * 40)\n",
        "print(\"ТОП-5 ЖАНРОВ КИНО (Movies):\")\n",
        "print(get_top_genres('Movie'))\n",
        "\n",
        "print(\"\\nТОП-5 ЖАНРОВ СЕРИАЛОВ (TV Shows):\")\n",
        "print(get_top_genres('TV Show'))"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "_aq7ml1NM2kW",
        "outputId": "cc5ae356-4bc7-4d08-b738-3b4adf4a5094"
      },
      "execution_count": 31,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "САМЫЕ ПОПУЛЯРНЫЕ ЖАНРЫ НА NETFLIX\n",
            "----------------------------------------\n",
            "ТОП-5 ЖАНРОВ КИНО (Movies):\n",
            "listed_in\n",
            "International Movies    2752\n",
            "Dramas                  2427\n",
            "Comedies                1674\n",
            "Documentaries            869\n",
            "Action & Adventure       859\n",
            "Name: count, dtype: int64\n",
            "\n",
            "ТОП-5 ЖАНРОВ СЕРИАЛОВ (TV Shows):\n",
            "listed_in\n",
            "International TV Shows    1351\n",
            "TV Dramas                  763\n",
            "TV Comedies                581\n",
            "Crime TV Shows             470\n",
            "Kids' TV                   451\n",
            "Name: count, dtype: int64\n"
          ]
        }
      ]
    }
  ]
}
