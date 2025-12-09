# projeto-6
# Nested RelationShip:

from rest_framework import serializers 
from .models import Evento, Participante, Atividade 

class EventoSerializer(serializers.ModelSerializer):
    class Meta:
        model = Evento
        fields = '__all__' 

class ParticipanteSerializer(serializers.ModelSerializer):
    class Meta:
        model = Participante
        fields = '__all__' 

class AtividadeSerializer(serializers.ModelSerializer):
    class Meta:
        model = Atividade
        fields = '__all__'

# NO SERIALIZERS CRIAR UM TREM.PY PARA CADA ENTIDADE, ANTES DE CRIAR O TREM.PY CRIA __INIT__.PY
# vai no participante_serializer.py

from rest_framework import serializers 
from eventos.models import Participante

class
participanteSerializer(serializers.ModelSerializer):
  class Meta:
    model = Participante
    filds = '__all__'

# atividade_seriaalizer.py

from rest_framework import serializers
from eventos,models import Atividade, Participante
from .participante_serializer import ParticipanteSerializer

class 
AtividadeSerializer(serializers.ModelSerializer):
  responsavel = 
    ParticipanteSerializer(read_only=True)
      responsavel_id=
    serializers.PrimaryKeyRelatedFild(

   quwryset=Participante.objects.all(),
            source='responsavel'
            write_only=True,
            required=False
  )
    class Meta:
      model = Atividade
      fields = '__all__'

      
# evento_seriaalizer.py

from rest_framework import serializers
from eventos,models import Evento
from .atividade_serializer import AtividadeSerializer
from .participante_serializer import ParticipanteSerializer


class 
EventoSerializer(serializers.ModelSerializer):
    class Meta:
      model = Evento
      fields = '__all__'

class 
EventoDetailSerializer(serializers.ModelSerializer):
  atividades -
AtiviidadeSerializer(many=True, read_only=True)
  participantes = ParticipanteSerializer(many=True, read_only=true)

  
  class Meta:
      model = Evento
      fields = [
        'id',
        'nome',
        'descrição', 
        'data_início', 
        'data_fim', 
        'local'
        'atividades',
        'participantes'
    ]

# ajustar o __init__.py

from .evento_serializer import EventoSerializer, EventoDetailSerializer
from .participanteSerializer import ParticipanteSerializer
from .ativiidadeSerializer import AtiviidadeSerializer

# na views.py em EventoViewSet substitua o serializers por 

def get_serializer_class(self):
  if self,action in ("retrieve","dashboardd"]:
    return EventoDetailSerializer
  return EventoSerializer
  
      
