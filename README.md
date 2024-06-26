{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/sukantjain/Python/blob/main/IMDLIB.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "**Script to download IMD Gridded data into CSV file**\n"
      ],
      "metadata": {
        "id": "3lKIfkwzQSFm"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "from google.colab import drive\n",
        "drive.mount('/content/drive')"
      ],
      "metadata": {
        "id": "8ymCHzEiP4L_"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "pip install imdlib"
      ],
      "metadata": {
        "id": "EGD59HRi9Qls"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "xnxDLwE99JvY"
      },
      "outputs": [],
      "source": [
        "import imdlib as imd\n",
        "\n",
        "path = \"/content/drive/MyDrive/Colab Notebooks\"\n",
        "\n",
        "start_yr = 2019\n",
        "end_yr = 2020\n",
        "variable = 'rain' # other options are ('tmin'/ 'tmax')\n",
        "\n",
        "imd.get_data(variable, start_yr, end_yr, fn_format='yearwise', file_dir=path)\n",
        "data = imd.open_data(variable, start_yr, end_yr,'yearwise', path)\n",
        "ds = data.get_xarray()\n",
        "print(ds)\n",
        "\n",
        "\n",
        "\n",
        "lat = 20.03 #lattitude of point\n",
        "lon = 77.23 #longitude of point\n",
        "data.to_csv('data.csv', lat, lon, path)"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Save CSV files for multiple points\n",
        "\n",
        "# Provide lat and long in a list\n",
        "latLong = [[20.3,77.23],[23.5,72.5],[26.0,77,1]]\n",
        "\n",
        "for points in latLong:\n",
        "  lat = points[0]\n",
        "  lon = points[1]\n",
        "\n",
        "  data.to_csv('test.csv', lat, lon, path)\n",
        "  print (\"data save for \",points)"
      ],
      "metadata": {
        "id": "kygArbTkBPMT"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
