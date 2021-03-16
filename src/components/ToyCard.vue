<template>
    <div class="card">
        <h2>{{'Toys Name'}}</h2>
        <img src='{toy image}' alt='{toy name}' class="toy-avatar" />
        <p>{{'likecount'}} Likes </p>
        // eslint-disable-next-line vue/no-parsing-error
        <button class="like-btn">Like {<3}</button>
        <button class="del-btn">Donate to GoodWill</button>
      </div>
</template>