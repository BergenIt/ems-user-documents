# Часто задаваемые вопросы по функционалу продукта (FAQ)

> <details>
> <summary style="background-color: #E5ECEB">Связанны ли логический и физический проводники в системе? </summary>
> <p></p>
> Физический и логический проводники являются разным отображением устройств в системе. Включают в себя ряд отличий по доступным представлениям информации данных устройств. 
> 
>   * Физический проводник системы представляет из себя фактическую структуру размещения устройств с наличием иерархии, которая формируется из зданий их помещений и серверных стоек. Формирование данной структуры осуществляется в физическом виде проводника системы. Изменение размещения устройства может быть выполнено в карточке самого устройства. 
>   * Логический проводник системы представляет из себя логическую группировку устройств, систем и серверных стоек, которые могут быть сформированны в зависимости от потребности пользователя. 
>
> 
> ***Описание процедуры по формированию структуры размещения оборудования, работы с проводниками системы и управление объектами проводника подробно представлено в пункте "5.4 Настройка отображения инфраструктуры" Руководства пользователя системы EMS.***
> </details>


 <p></p>


> <details>
> <summary style="background-color: #E5ECEB">Можно ли синхронизировать структуру логического проводника с физическим?  </summary>
> <p></p>
> Система позволяет синхронизировать структуру логического проводника с физическим. В данном случае, при создании объектов физического проводника, таких как здание, помещение, стойка, данная структура будет созданна и в логическом проводнике в виде вложенных директорий. Следуюет учитывать, что синхронизация будет применена только к структуре, которая создается после включении данной функции. 
> 
> ***Описание процедуры по синхронизации структуры логического проводника с физическим представлено в пункте "5.4 Настройка отображения инфраструктуры" Руководства пользователя системы EMS.***
> </details>


<p></p>


> <details>
> <summary style="background-color: #E5ECEB">Можно ли реализовать доступ к устройствам для конкретного пользователя? </summary>
> <p></p>
> Для организации распределенного доступа к оборудованию, необходимо предварительно сформировать структуру размещения оборудования в физическом проводнике системы и синхронизировать эту структуру с логическим проводником. Разграничить доступ можно на уровне директорий логического проводника, которые при синхронизации являются эквивалентом зданий, помещений и серверных стоек. Также при необходимости, система позволяет настроить изолированный доступ к разному оборудования в рамках одной серверной стойки.
> </details>

<p></p>

> <details>
> <summary style="background-color: #E5ECEB">Требуется ли использовать разные роли для пользователей в системе? </summary>
> <p></p>
> Для обеспечения сохранности данных, настроек и избежания рисков при взаимодействии с оборудованием рекомендуется разделять доступ к функционалу по управлению, мониторингу, согласованию и администрированию системы на разные роли, которые будут назначены разным пользователям. 
> 
> ***Описание процедуры по созданию ролей и добавления ресурсов подробно представлено в пункте "5.2.5 Создание роли" Руководства пользователя системы EMS.***
> </details>


<p></p>


> <details>
> <summary style="background-color: #E5ECEB">Какие есть ограничения при многопользовательской работе в системе?  </summary>
> <p></p>
> Для обеспечения корректной работы системы не рекомендуется осуществлять одновременную работу нескольких пользователей на одном устройстве в следующем функционале: 
> 
>   * Обновление прошивок BMC и UEFI;
>   * Установка ПО; 
>   * Выполнение скрипта на устройстве;
>   * Установка операционной системы;
>   * Ручное создание резервной копии системы;
>   * Редактирование структуры логического проводника в части перемещения объектов (стойка, устройство, система);
>   * Редактирование сущности справочного каталога;
>   * Редактирование сущности файлового репозитория. 
> 
> Для того, что бы избежать возможных ошибок, а также потери данных рекомендуется разграничивать доступы пользователей к функционалу системы посредством ролевой модели. 
> </details>


<p></p>

